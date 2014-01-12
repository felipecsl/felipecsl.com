---
comments: true
date: 2009-06-17 16:23:00
layout: post
slug: hiding-sensitive-data-in-the-query-string
title: Hiding sensitive data in the query string
wordpress_id: 34
---

Sometimes you need to pass data to a web page and at the same time you need to be able to provide a permalink to that URL to the user. In this case, you don't have any option other than passing those parameters through the Query String. Otherwise, you could use the Form, Session state, database or any other persistence or data transport mechanism.

I recently had to create a page that needed to receive some sensitive parameters and, at the same time, I needed to be able to provide the URL to the user, so that he/she could view that same page. However, I needed to somehow make the parameters private to the system, so that no one could decypher what data the actual parameters held. The only solution I found was to [encrypt](http://en.wikipedia.org/wiki/Cryptography) the Query String values!

For those who are not very familiar with the subject (like me), cryptography can be a really scary thing! Thankfully, Jeff Atwood, founder of the famous [codinghorror.com](/admin/Pages/www.codinghorror.com) blog (which of I am a fan also!) wrote a great [article](http://www.codeproject.com/KB/security/SimpleEncryption.aspx) at Code Project with some simple background, definitions and a .NET code for those who do not have a strong background on the subject.

I not only found that very useful but also ported the code to C# to fulfill my needs. [This tool](http://www.developerfusion.com/tools/convert/vb-to-csharp/) helped me with the rough conversion but I still had to do some conversion by hand, since the code did not compile at first try.

I separated the code logically in different files for better reading. It can be downloaded [here](http://www.felipel.com/files/Encryption.zip).

Below is a simple usage of the Simmetric-key class with the Rijndael ([AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)) provider to encrypt the query string variable in one page, send it, and then decrypt in the other side:
    
    <span class="lnum">   1:  </span>Symmetric symEncryption = <span class="kwrd">new</span> Symmetric(Symmetric.Provider.Rijndael);
    
    <span class="lnum">   2:  </span>symEncryption.Key.Text = <span class="str">"SomeKey"</span>;
    
    <span class="lnum">   3:  </span> 
    
    <span class="lnum">   4:  </span><span class="kwrd">string</span> sSensitiveText = <span class="str">"Some sensitive data"</span>;
    
    <span class="lnum">   5:  </span><span class="kwrd">string</span> sEncryptedData = symEncryption.Encrypt(<span class="kwrd">new</span> Data(sSensitiveText)).Base64;
    
    <span class="lnum">   6:  </span> 
    
    <span class="lnum">   7:  </span><span class="rem">// fearlessly send sEncryptedData in your query string</span>
    
    <span class="lnum">   8:  </span>Response.Redirect(
    
    <span class="str"><span style="white-space: pre" class="Apple-tab-span">	</span>"http://www.someurl.com/somepage.aspx?data="</span> + Server.UrlEncode(sEncryptedData));
    
    <span class="lnum">   9:  </span> 
    
    <span class="lnum">  10:  </span>...
    
    <span class="lnum">  11:  </span> 
    
    <span class="lnum">  12:  </span><span class="rem">// in the other side, decrypt the text you just received</span>
    
    <span class="lnum">  13:  </span><span class="kwrd">string</span> sDecryptedText = symEncryption.Decrypt(
    
    <span class="kwrd"><span style="white-space: pre" class="Apple-tab-span">	</span>new</span> Data(Request.QueryString[<span class="str">"data"</span>].FromBase64())).Text;
    
    <span class="lnum">  14:  </span> 
    
    <span class="lnum">  15:  </span><span class="rem">// outputs "Some sensitive data"</span>
    
    <span class="lnum">  16:  </span>Console.WriteLine(sDecryptedText); 

  
Hope this helps someone :)
