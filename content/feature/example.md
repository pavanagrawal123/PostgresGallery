---
title: "My Shiny Example"
Date: "2015-01-17"
---


### Description
The code changes the Style properties of the Block and configures it such that Scrollbars will be shown only when overflow is present.
### Code
<style>
  .block-class{overflow:auto;max-height:400px;}
</style>
{{< highlight sql class='block-class' >}}
SELECT * FROM test
{{< / highlight >}}

### Code Breakdown and Explanation
1st:
  Let the class to which the SQL Code blocks belong to be '.block-class'

2nd:
  Now in the Stylesheet we change the overflow property to 'auto', it means scrollbars will be added only when content overflows.
  'max-height' property determines to upto what extent the Block's height can expand. If the content's length is found to more than 'max-height', then scrollbars will be added.

3rd:
  Extra attribute to the markup of the block. 'class' property assigns a class to the block. And all the styling properties will be inherited by the block (which are written is stylesheet).
