---
comments: true
date: 2009-08-20 06:43:00
layout: post
slug: copying-linq-non-datarow-query-results-to-datatable
title: Copying Linq (non-DataRow) query results to DataTable
wordpress_id: 24
---

How to use the results of a database query using Linq to fill a DataGrid? It should be no big deal since there is a useful [CopyToDataTable](http://msdn.microsoft.com/en-us/library/bb396189.aspx) extension method:
    
    <span class="lnum">   1:  </span><span class="kwrd">public</span> <span class="kwrd">static</span> DataTable CopyToDataTable<T>(
    
    <span class="lnum">   2:  </span>    <span class="kwrd">this</span> IEnumerable<T> source
    
    <span class="lnum">   3:  </span>)
    
    <span class="lnum">   4:  </span><span class="kwrd">where</span> T : DataRow

However, there is a problem: **T has to be a DataRow**. When returning query results from the database, especially with EF, your query results are not DataRows (and I wonder if the same is true for Linq to Sql too). So, in this case, you'll have to fill the DataTable by hand. Thanks to this [good blog post](http://unboxedsolutions.com/sean/archive/2009/06/06/15961.aspx), I was able to fill it:
    
    <span class="lnum">   1:  </span>DataTable dataTable = <span class="kwrd">new</span> DataTable();
    
    <span class="lnum">   2:  </span>dataTable.TableName = <span class="str">"ResultsTable"</span>;
    
    <span class="lnum">   3:  </span>dataTable.Columns.Add(<span class="str">"User"</span>, <span class="kwrd">typeof</span>(<span class="kwrd">string</span>));
    
    <span class="lnum">   4:  </span>dataTable.Columns.Add(<span class="str">"TotalJobs"</span>, <span class="kwrd">typeof</span>(<span class="kwrd">int</span>));
    
    <span class="lnum">   5:  </span> 
    
    <span class="lnum">   6:  </span>var query = <span class="rem">/* your linq query comes here. no restrictions! */</span>

we have the DataTable and the query set up. Now, the tricky part! 
    
    <span class="lnum">   1:  </span>var results = query.Select(anonym => <span class="kwrd">new</span> Func<DataRow, <span class="kwrd">int</span>, <span class="kwrd">int</span>, DataRow>(
    
    <span class="lnum">   2:  </span>    (DataRow row, <span class="kwrd">int</span> index, <span class="kwrd">int</span> count) =>
    
    <span class="lnum">   3:  </span>    {
    
    <span class="lnum">   4:  </span>        row[<span class="str">"User"</span>] = index;
    
    <span class="lnum">   5:  </span>        row[<span class="str">"TotalJobs"</span>] = count;
    
    <span class="lnum">   6:  </span>        <span class="kwrd">return</span> row;
    
    <span class="lnum">   7:  </span>    })
    
    <span class="lnum">   8:  </span>    .Invoke(dataTable.NewRow(), anonym.Index, anonym.TotalJobs));
    
    <span class="lnum">   9:  </span> 
    
    <span class="lnum">  10:  </span>results.ToList().ForEach(row => dataTable.Rows.Add(row));

Absolutely a good piece of unreadable code :)

_query _variable are your Linq query results, which may be an IEnumerable of some of your data entities or even a anonymous type. It doesn't matter! For each element of this enumeration, we're creating a DataRow and assigning some values to its columns. Then, we call _Invoke _to indeed invoke our anonymous delegate Func, passing in our anonymous type properties, that are used later to fill the DataTable.

You'll probably gonna need to read it a couple times to digest it a bit and still it will look "WTF did I really wrote this code?!?" after a couple days :) 
