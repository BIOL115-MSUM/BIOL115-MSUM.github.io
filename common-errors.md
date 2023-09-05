# Common Errors

When you run R code, you may sometimes see messages, warnings, or errors appear in the console.

Errors appear as red text beginning with the word "Error".

See below for examples of common errors:

+-----------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Error message                                                               | Example code generating error                                  | Explanation and how to fix                                                                                                                        |
+=============================================================================+================================================================+===================================================================================================================================================+
| ```                                                                         | ```                                                            | The function ggsave does not recognize the argument named length. You probably changed the word "height" to "length" using the Find/Replace tool. |
| Error in check.options(new, name.opt = ".X11.Options", envir = .X11env) :   | ggsave("rame_length_bar_chart.png", width = 2.5, length = 3.5) |                                                                                                                                                   |
|   invalid argument name ‘length’ in 'png_dev(..., res = dpi, units = "in")' | ```                                                            | Change the word "length" back to "height"                                                                                                         |
| ```                                                                         |                                                                |                                                                                                                                                   |
+-----------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
|                                                                             |                                                                |                                                                                                                                                   |
+-----------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
|                                                                             |                                                                |                                                                                                                                                   |
+-----------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+