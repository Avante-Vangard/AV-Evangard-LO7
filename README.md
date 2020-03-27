# Evangard SFM
_Build a better Libre Office Writer document._

This is zero rev code, or idea collation only. 

This project is not ready. 

## Simplified Flow

__1. Write text (text based.. or simplified view. not WYSIWYG)__

  _a. USFM vs. p.sfm_

__2. Choosing Fonts in LibreOffice Writer.__

  _a. built in or build in smcp, c2sc, onum, lnum._
  
  _b. normalize fonts to same em._

__3. Build stylesheet in LibreOffice Calc.__

  _a. Shaping_
  
All fonts should be scaled so the height of a capital X matches the Cormorant font.
  
All fonts used should be scaled for width appropriately.  Usually this means matching the width of cormorant for the string "ABCDEFGabcdefg" or a similar short 10-12 character sample. However, The point is the fonts look normal in the final work, so you'll want to vary the x scaling to achieve the correct look.

The webpage (Font drop|https://fontdrop.info/) provides the true ___Font___, ___Face___, and ___Weight___ class that LibreOffice needs. 

The ___Weight___ field is 100-900 defined in the font.  However, the text "bold" will cause LibreOffice to generate a bold face from the regular face if the font has no 700 class weight available. 

The ___Skew___ field is "normal" or "italic". LibreOffice will use an italic face if it exists, or skew the regular face if no italic exists for the font defined. 
  
  _b. Sizing_
  
  The configuration page in the Calc sheet contains 3 main settings: Point size, leading ratio, and scaling ratio. The point size is that of the font's design box, not the height or width of the text. To have 8pt text you should measure the cap height is 8 pts. The scaling and leading ratios are multiples of this design box number. leading ratio is constant for all sizes, The scaling is multiples.  
  
  _c. Styling_

Once you have the fonts and base sizes defined, then you can customize the stylesheet (active styles) and the rest of the configuration page to acheive the look of the work. After each change, you need to manually recalc (f9 in linux), as autocalc causes serious issues in near-endless loops this file has.

The fields on the active style page

___Base___ is the paragraph style to follow when no other style is defined. Valid entries appear in the ___Tag___ column (column W as of this writing). 

___Face___ is the __IDX___ from the Active fonts page describing the text style and weight.

___Vert___ is the ___DY___ column from the Base Pts Page describing the vertical size for the style. 

___Horz___ is the ___DX___ column from the Base Pts Page describing the horizontal attributes for the style. 

___Extra and X2___ is the ___EX___ column from the Base Pts Page and describes the other attributes for the style. 

___Sort__ : an Entry of "V" in the Sort Column of Active Styles causes a variable with the tag name to be created in the stylesheet. 

_d. Save your stylesheet_
  
When you're stylesheet is ready, copy all the text on the LO-Stylesheet pane, and past it into a plain text document.  Save that text as __yourstyle.fodt__, and open that file.  You should be able to see your defined page size, and all your styles in the styles pane. 

__4. Weld text to styles via Jedit.__

Vangard Libre uses Jedit for conversion. If you study the process, this process could just as easily be accomplished with a finalchanges file. The intended final solution is an import filter in LibreOffice Writer that does all of this. 

The Jedit setup includes 3 things: 1) a syntax file for p.sfm that goes into the jedit /modes folder, 2) a macro for inserting character tags, and 3) the SFM>ODT macro. 

  _a. Concatenation of sfm files._

If you have more than one file that will go into your work, you may wish to concatenate them first.  in unix, this is simply $cat *.sfm > myfile.p.sfm   

  _b. Pre-conversion stuff._

p.sfm needs : 

header defaults to the tags h and cn.  You may want to duplicate toc if your file doesn't have an h tag. Also, the macro is only aware of the h and toc tags inside the file,  if you've updated the table in paratext after initial setup, you may need to synchronize the paratext table back into the  individual files before proceeding. The tag cn attempts to use the intended chapter number that prints at the chapter boundary, whether this was c, cp or cl in the sfm file. cl tags are only supported in their 'late' form. You need a cl each chapter you want to have a label. 

For two column text, the end of each file needs an end marker inserted with the tag \mte9 ~ . Additionally, the h and toc tags should be zeroed a the end of each book (\h ~, \toc ~, etc.) 

  _c. Convert (run the macro.)_

  _d. Import stylesheet._

  _e. Move End-of-File to bottom._
  
__5. Prepare Text in LibreOffice Writer._

  _a. Flow and check._ Fix in the source files as much as possible.

  _b. Fixing in Writer_
  
The tracking field is the primary push/pull tool to fit troublesome text. 

  _d. Finish_

This methodology is still in development. 
