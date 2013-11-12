---
comments: true
date: 2009-07-27 11:09:00
layout: post
slug: dynamically-adding-user-controls-to-web-page-with-asp-net
title: Dynamically adding user controls to web page with ASP.NET
wordpress_id: 29
---

I've been very busy lately and unfortunately didn't have enough time to stop here to write about things I have been working on. There are other subjects that I'd like to talk about but, for now, I'll share my findings with asp.net user controls dynamically added to the page, difficulties, limitations and solutions.  

  

I'm working on a Ajax based web site that basically contains a content area in the right, where I need to put the dynamic content, based on the user selection on the left menu. The ongoing work can be seen [here](/admin/Pages/www.felipel.com/visiocore/ContentPage.aspx).  

  

The easier way to do this is to create an asp.net UserControl for the content of each page and to dynamically add each control to the page based on the user selection. I also added an UpdateProgress panel for better user experience. However, here is where the problems start. First off, you cannot simply instantiate an asp.net UserControl through its constructor and add it to the page. That won't work. Instead, you'll need to use the factory method Page.LoadControl(), providing it the virtual path to your control so that it returns the instance for you. Eg.:  

  






    
    
    <span class="lnum">   1:  </span>Control c = <span class="kwrd">this</span>.LoadControl(<span class="str">"~/MyUserControl.ascx"</span>);   <span class="rem">// Instantiate the user control</span>
    



    
    
    <span class="lnum">   2:  </span><span class="kwrd">this</span>.ContentArea.Controls.Add(c);    // Add it to the placeholder
    





  

Here, we're instantiating the control and adding it to the page. So far, so good. But, what happens if your user control needs to execute some javascript function upon loading? Even if you explicitly put <script> tags in your user control markup, it won't be executed at this time, so the solution is to use RegisterStartupScript to execute the client code:  

  






    
    
    <span class="lnum">   1:  </span>ClientScript.RegisterStartupScript(<span class="kwrd">typeof</span>(<span class="kwrd">this</span>), <span class="str">"some script key"</span>, <span class="str">"<script type="</span>text/javascript<span class="str">">alert('hello world!');</script>"</span>);
    





  

or, if you're using Ajax, use the ScriptManager static method:  

  






    
    
    <span class="lnum">   1:  </span>ScriptManager.RegisterStartupScript(<span class="kwrd">this</span>, <span class="kwrd">typeof</span>(<span class="kwrd">this</span>), <span class="str">"some script key"</span>, <span class="str">"<script type="</span>text/javascript<span class="str">">alert('hello world!');</script>"</span>, <span class="kwrd">false</span>);
    





  

Put this and your user control will show up smoothly. If you don't like the fact that the screen may remain unresponsive for some time with Ajax, you can use UpdateProgress to show a "Loading" text, for example, while the content is being loaded. This is fairly easy. Check out this [video](http://www.asp.net/learn/ajax-videos/video-123.aspx)  for further information.  

  

Okay, so now, what happens if we need to fire an event inside the UserControl in response to a user click on an image, for example? Right, the click event will fire a page postback and then the event handling code will be fired in the code behind as expected. Right? Definitely no! Since our user controls are being added dynamically to the page, they will not be there anymore after the postback. This means that ASP.Net will not find the control and, therefore, no event will be fired.  

  

Let me refresh some facts about ASP.Net postback functionality before continuing... Whenever you click a server control in the page, javascript __doPostBack function is called (except for Button and ImageButton, that use a different method - form post). The __doPostBack function takes two arguments, eventTarget and eventArgument. The eventTarget contains the ID of the control that causes the postback and the eventArgument contains any additional data associated with the control. Upon page reload, ASP.Net checks both Request.Params["__EVENTTARGET"] and Request.Params["__EVENTARGUMENT"] parameters for any postback data. If it finds it, it looks for the control ID and method specified in the __EVENTTARGET var and calls the specified method, passing the __EVENTARGUMENT value as a parameter.  

  

Said that and knowing that our dynamic user control won't be present in the page during the postback, it is easy to conclude that ASP.Net won't find the control for the ID in the __EVENTTARGET parameter and, consequently, nothing will happen.  

  

Okay, so we need to re-add our user control to the page during the postback, so that ASP.Net will be able to find it and fire its event handler. In order to accomplish that, we can use the page ViewState to store the name of the control currently in the page, so that we can re-add it in the page OnLoad event.  

  






    
    
    <span class="lnum">   1:  </span><span class="kwrd">protected</span> <span class="kwrd">override</span> <span class="kwrd">void</span> OnLoad(EventArgs e)
    



    
    
    <span class="lnum">   2:  </span>{
    



    
    
    <span class="lnum">   3:  </span>    <span class="kwrd">base</span>.OnLoad(e);
    



    
    
    <span class="lnum">   4:  </span>
    



    
    
    <span class="lnum">   5:  </span> 
    



    
    
    <span class="lnum">   6:  </span>    <span class="kwrd">if</span> (!<span class="kwrd">this</span>.IsPostBack)
    



    
    
    <span class="lnum">   7:  </span>    {
    



    
    
    <span class="lnum">   8:  </span>        <span class="rem">// If this is not a postback, set our the initial content page</span>
    



    
    
    <span class="lnum">   9:  </span>        ChangeSection(<span class="str">"~/InitialControl.ascx"</span>);
    



    
    
    <span class="lnum">  10:  </span>    }
    



    
    
    <span class="lnum">  11:  </span>    <span class="kwrd">else</span>
    



    
    
    <span class="lnum">  12:  </span>    {
    



    
    
    <span class="lnum">  13:  </span>        <span class="rem">// Else, retrieve the CurrentControl value from the ViewState</span>
    



    
    
    <span class="lnum">  14:  </span>        <span class="kwrd">string</span> currentSection = ViewState[<span class="str">"CurrentControl"</span>] <span class="kwrd">as</span> <span class="kwrd">string</span>;
    



    
    
    <span class="lnum">  15:  </span>        Control c = ChangeSection(currentSection);    <span class="rem">// Use the control name to add it to the page</span>
    



    
    
    <span class="lnum">  16:  </span> 
    



    
    
    <span class="lnum">  17:  </span>        <span class="kwrd">if</span> (c <span class="kwrd">is</span> Eventos_EventosRealizados)
    



    
    
    <span class="lnum">  18:  </span>        {
    



    
    
    <span class="lnum">  19:  </span>            ((Eventos_EventosRealizados)c).UpdateCallback = delCallback;
    



    
    
    <span class="lnum">  20:  </span>        }
    



    
    
    <span class="lnum">  21:  </span>    }
    



    
    
    <span class="lnum">  22:  </span>}
    



    
    
    <span class="lnum">  23:  </span> 
    



    
    
    <span class="lnum">  24:  </span><span class="kwrd">public</span> Control ChangeSection(<span class="kwrd">string</span> _sControl)
    



    
    
    <span class="lnum">  25:  </span>{
    



    
    
    <span class="lnum">  26:  </span>    Control c = <span class="kwrd">this</span>.LoadControl(_sControl);
    



    
    
    <span class="lnum">  27:  </span>
    



    
    
    <span class="lnum">  28:  </span>    <span class="rem">// Put a 3 seconds delay so that we can see the magic happen -- remove in the final version</span>
    



    
    
    <span class="lnum">  29:  </span>    System.Threading.Thread.Sleep(3000);
    



    
    
    <span class="lnum">  30:  </span> 
    



    
    
    <span class="lnum">  31:  </span>    <span class="kwrd">this</span>.ContentArea.Controls.Add(c);    <span class="rem">// Add the control to the page</span>
    



    
    
    <span class="lnum">  32:  </span> 
    



    
    
    <span class="lnum">  33:  </span>    <span class="rem">// Important: Set its ID or the event might not be fired,</span>
    



    
    
    <span class="lnum">  34:  </span>    <span class="rem">// since ASP.Net uses the control ID to find it</span>
    



    
    
    <span class="lnum">  35:  </span>    c.ID = <span class="str">"ContentUserControl"</span>;
    



    
    
    <span class="lnum">  36:  </span> 
    



    
    
    <span class="lnum">  37:  </span>    ViewState[<span class="str">"CurrentControl"</span>] = _sControl;  <span class="rem">// store the control name in the ViewState</span>
    



    
    
    <span class="lnum">  38:  </span>
    



    
    
    <span class="lnum">  39:  </span>    <span class="rem">// Execute some javascript routine to refresh the screen (if needed)</span>
    



    
    
    <span class="lnum">  40:  </span>    ScriptManager.RegisterStartupScript(<span class="kwrd">this</span>, <span class="kwrd">typeof</span>(<span class="kwrd">this</span>), <span class="str">"some script key"</span>, <span class="str">"<script type="</span>text/javascript<span class="str">">refreshPage();</script>"</span>, <span class="kwrd">false</span>);
    



    
    
    <span class="lnum">  41:  </span> 
    



    
    
    <span class="lnum">  42:  </span>    <span class="kwrd">return</span> c;
    



    
    
    <span class="lnum">  43:  </span>}
    





  

So these are just some basic guidelines for handling user controls dynamically. If you need further info, [asp.net](http://asp.net) official website is always a great place to start off and watch with some videos.  

  

Till next time!

