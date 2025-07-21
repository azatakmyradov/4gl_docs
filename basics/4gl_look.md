[Index](index.html)  [Home](getting-started_home.html)

Look

`Look` can be used to check the existence of data in the database for a condition. It behaves exactly as the [Read](4gl_read.html) operations and has the same syntax. The only differences are the following:  
\* The variables present in the [F] class are not modified.  
\* `Look` cannot be used on joins declared with the [Link](4gl_link.html) instruction.  
\* `Look` does not allow you to know if the record is locked. The only solution is to check the user's [Readlock](4gl_readlock.html).

After the execution of `Look`:  
\* [fstat](4gl_fstat.html) is updated with the same values as [Read](4gl_read.html).  
\* The current line becomes the line found. Consequently, a [Read](4gl_read.html) Curr will fill the [F] record with the result of the line found through the look operation. Note, If `Look` returns an `fstat` error, the subsequent [Read](4gl_read.html) Curr results are unpredictable.

With SQL server, `Look` uses a dynamic cursor regardless of whether or not [With](4gl_with.html) [Stability](4gl_stability.html) is specified.

For more information, see the [Read](4gl_read.html) document.

# See also

[Readlock](4gl_readlock.html), [File](4gl_file.html), [Link](4gl_link.html), [Filter](4gl_filter.html), [Columns](4gl_columns.html), [For](4gl_for.html), [Rewrite](4gl_rewrite.html), [RewriteByKey](4gl_rewritebykey.html), [Delete](4gl_delete.html), [DeleteByKey](4gl_deletebykey.html), [Update](4gl_update.html), [Look](4gl_look.html), [Write](4gl_write.html), [fstat](4gl_fstat.html), [currind](4gl_currind.html), [currlen](4gl_currlen.html), [With](4gl_with.html), [Stability](4gl_stability.html).

  

[Index](index.html)  [Home](getting-started_home.html)