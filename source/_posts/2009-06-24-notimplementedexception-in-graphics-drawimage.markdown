---
comments: true
date: 2009-06-24 11:13:00
layout: post
slug: notimplementedexception-in-graphics-drawimage
title: NotImplementedException in Graphics.DrawImage
wordpress_id: 33
---


It is a bit weird to notice that a .Net Framework method returns NotImplementedException. At least it was for me, mainly because it is not documented anywhere in the msdn documentation.






It turns out that Graphics.DrawImage throws this exception when an Image object is passed in. This is really funny, since this method actually expects an Image object as its first argument, so my first-try code to print an image file was:








    
    
    <span class="lnum">   1:  </span><span class="kwrd">public</span> <span class="kwrd">void</span> PrintImage(<span class="kwrd">string</span> fileName)
    



    
    
    <span class="lnum">   2:  </span> 
    



    
    
    <span class="lnum">   3:  </span>{
    



    
    
    <span class="lnum">   4:  </span> 
    



    
    
    <span class="lnum">   5:  </span>      Image img = Image.FromFile(fileName);
    



    
    
    <span class="lnum">   6:  </span>      PrintDocument printDoc = <span class="kwrd">new</span> PrintDocument();
    



    
    
    <span class="lnum">   7:  </span>      printDoc.DocumentName = <span class="kwrd">this</span>.m_sFilename;
    



    
    
    <span class="lnum">   8:  </span>      printDoc.PrintPage += <span class="kwrd">new</span> PrintPageEventHandler(PrintPage);
    



    
    
    <span class="lnum">   9:  </span>      printDoc.Print();
    



    
    
    <span class="lnum">  10:  </span> 
    



    
    
    <span class="lnum">  11:  </span>}
    



    
    
    <span class="lnum">  12:  </span> 
    



    
    
    <span class="lnum">  13:  </span><span class="kwrd">private</span> <span class="kwrd">void</span> PrintPage(<span class="kwrd">object</span> sender, PrintPageEventArgs e)
    



    
    
    <span class="lnum">  14:  </span>{
    



    
    
    <span class="lnum">  15:  </span>      <span class="rem">// Throws NotImplementedException!!!</span>
    



    
    
    <span class="lnum">  16:  </span> 
    



    
    
    <span class="lnum">  17:  </span>      e.Graphics.DrawImage(
    



    
    
    <span class="lnum">  18:  </span>           <span class="kwrd">this</span>.printedImage,
    



    
    
    <span class="lnum">  19:  </span>           <span class="kwrd">new</span> Point(e.MarginBounds.Left, e.MarginBounds.Top));
    



    
    
    <span class="lnum">  20:  </span> 
    



    
    
    <span class="lnum">  21:  </span>      e.HasMorePages = <span class="kwrd">false</span>;
    



    
    
    <span class="lnum">  22:  </span>}
    








Weird, eh?! So, the solution? 














    
    
    <span class="lnum">   1:  </span>Bitmap img = (Bitmap)Image.FromFile(fileName);
    








Bitmap class extends Image, so, IMHO, DrawImage should determine in runtime that the image passed in is actually is a Bitmap and do whatever it has to do, but, strangely, it complains and throws a NotImplementedException for the exactly same runtime object.






Can someone explain what is happening here?




