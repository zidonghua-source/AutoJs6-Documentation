# Color List (Color Table)

The color list provides color information corresponding to color names (Hex code, RGB components, HSV components, etc.).

Color names are also called color keywords. For example, `black` represents black, `blue` represents blue, etc.  
In the [CSS](https://en.wikipedia.org/wiki/CSS) color definitions, there are 148 color keywords in total. Their names originate from the [X Window System](https://en.wikipedia.org/wiki/X_Window_System) (also known as `X11`), so these color names are also called [X11 colors](https://en.wikipedia.org/wiki/X11_color_names). See the [CSS Color List](#css-color-list) section for details.

> Note: The HSV components in the list are rounded approximate values for reference only.  
> When converted to the corresponding color as a parameter, there may be slight deviations from the original color.

## Android Color List

Android's `android.graphics.Color` class provides a mapping between some color names and color integer values, stored in the private variable `sColorNameMap`.

The following color list converts the color names into variable names, which can be accessed directly through the global `colors` object.

Usage:

```js
colors.android.BLACK;
colors.BLACK; /* Same as above. */
colors.toInt('black'); /* Same as above, case-insensitive. */

colors.android.DARK_GRAY;
colors.DARK_GRAY; /* Same as above. */
colors.toInt('darkgray'); /* Same as above, case-insensitive. */
```

|                       Color                       | Variable Name                                                | English Name                                      | Hex Code    | RGB                                                    | HSV                                                    |
|:-------------------------------------------------|--------------------------------------------------------------|---------------------------------------------------|-------------|--------------------------------------------------------|--------------------------------------------------------|
|  <p style="background-color: #000000">　　　</p>  | BLACK                                                        | Black                                             | #000000     | 0,0,0                                                  | 0,0,0                                                  |
|  <p style="background-color: #0000FF">　　　</p>  | BLUE                                                         | Blue                                              | #0000FF     | 0,0,255                                                | 240,100,100                                            |
|  <p style="background-color: #00FFFF">　　　</p>  | <span style="white-space:nowrap">CYAN / AQUA</span>          | Cyan / Aqua                                       | #00FFFF     | 0,255,255                                              | 180,100,100                                            |
|  <p style="background-color: #444444">　　　</p>  | DARK_GRAY<br/>DARK_GREY<br/>DKGRAY                           | Dark Gray                                         | #444444     | 68,68,68                                               | 0,0,27                                                 |
|  <p style="background-color: #888888">　　　</p>  | GRAY<br/>GREY                                                | Gray                                              | #888888     | 136,136,136                                            | 0,0,53                                                 |
|  <p style="background-color: #00FF00">　　　</p>  | <span style="white-space:nowrap">GREEN / LIME</span>         | Green / Lime                                      | #00FF00     | 0,255,0                                                | 120,100,100                                            |
|  <p style="background-color: #CCCCCC">　　　</p>  | LIGHT_GRAY<br/>LIGHT_GREY<br/>LTGRAY                         | Light Gray                                        | #CCCCCC     | 204,204,204                                            | 0,0,80                                                 |
|  <p style="background-color: #FF00FF">　　　</p>  | <span style="white-space:nowrap">MAGENTA / FUCHSIA</span>    | Magenta / Fuchsia                                 | #FF00FF     | 255,0,255                                              | 300,100,100                                            |
|  <p style="background-color: #800000">　　　</p>  | MAROON                                                       | Maroon                                            | #800000     | 128,0,0                                                | 0,100,50                                               |
|  <p style="background-color: #000080">　　　</p>  | NAVY                                                         | Navy                                              | #000080     | 0,0,128                                                | 240,100,50                                             |
|  <p style="background-color: #808000">　　　</p>  | OLIVE                                                        | Olive                                             | #808000     | 128,128,0                                              | 60,100,50                                              |
|  <p style="background-color: #800080">　　　</p>  | PURPLE                                                       | Purple                                            | #800080     | 128,0,128                                              | 300,100,50                                             |
|  <p style="background-color: #FF0000">　　　</p>  | RED                                                          | Red                                               | #FF0000     | 255,0,0                                                | 0,100,100                                              |
|  <p style="background-color: #C0C0C0">　　　</p>  | SILVER                                                       | Silver                                            | #C0C0C0     | 192,192,192                                            | 0,0,75                                                 |
|  <p style="background-color: #008080">　　　</p>  | TEAL                                                         | Teal                                              | #008080     | 0,128,128                                              | 180,100,50                                             |
|  <p style="background-color: #FFFFFF">　　　</p>  | WHITE                                                        | White                                             | #FFFFFF     | 255,255,255                                            | 0,0,100                                                |
|  <p style="background-color: #FFFF00">　　　</p>  | YELLOW                                                       | Yellow                                            | #FFFF00     | 255,255,0                                              | 60,100,100                                             |
| <p style="background-color: #00000000">　　　</p> | TRANSPARENT                                                  | Transparent                                       | #00000000   | <span style="white-space:nowrap">0,0,0,0 (RGBA)</span> | <span style="white-space:nowrap">0,0,0,0 (HSVA)</span> |

## CSS Color List

CSS color names are also called CSS color keywords. They represent a specific color value.  
For example, in the CSS syntax `color:red`, `red` is a color keyword.

Before CSS3 there were 17 color keywords. CSS3 expanded this to 147, and CSS4 added 1 more, for a total of 148.

Usage:

```js
colors.css.ORANGE_RED;
```

|                      Color                      | Variable Name                                                | English Name                                      | Hex Code  | RGB         | HSV         |
|:-----------------------------------------------:|--------------------------------------------------------------|---------------------------------------------------|-----------|-------------|-------------|
| <p style="background-color: #F0F8FF">　　　</p> | ALICE_BLUE                                                   | Alice Blue                                        | #F0F8FF   | 240,248,255 | 208,6,100   |
| <p style="background-color: #FAEBD7">　　　</p> | ANTIQUE_WHITE                                                | Antique White                                     | #FAEBD7   | 250,235,215 | 34,14,98    |
| <p style="background-color: #7FFFD4">　　　</p> | AQUAMARINE                                                   | Aquamarine                                        | #7FFFD4   | 127,255,212 | 160,50,100  |
| <p style="background-color: #F0FFFF">　　　</p> | AZURE                                                        | Azure                                             | #F0FFFF   | 240,255,255 | 210,100,100 |
| <p style="background-color: #F5F5DC">　　　</p> | BEIGE                                                        | Beige                                             | #F5F5DC   | 245,245,220 | 60,10,96    |
| <p style="background-color: #FFE4C4">　　　</p> | BISQUE                                                       | Bisque                                            | #FFE4C4   | 255,228,196 | 33,23,100   |
| <p style="background-color: #000000">　　　</p> | BLACK                                                        | Black                                             | #000000   | 0,0,0       | 0,0,0       |
| <p style="background-color: #FFEBCD">　　　</p> | BLANCHED_ALMOND                                              | Blanched Almond                                   | #FFEBCD   | 255,235,205 | 36,20,100   |
| <p style="background-color: #0000FF">　　　</p> | BLUE                                                         | Blue                                              | #0000FF   | 0,0,255     | 240,100,100 |
| <p style="background-color: #8A2BE2">　　　</p> | BLUE_VIOLET                                                  | Blue Violet                                       | #8A2BE2   | 138,43,226  | 271,81,89   |
| <p style="background-color: #A52A2A">　　　</p> | BROWN                                                        | Brown                                             | #A52A2A   | 165,42,42   | 0,75,65     |
| <p style="background-color: #DEB887">　　　</p> | BURLY_WOOD                                                   | Burly Wood                                        | #DEB887   | 222,184,135 | 34,39,87    |
| <p style="background-color: #5F9EA0">　　　</p> | CADET_BLUE                                                   | Cadet Blue                                        | #5F9EA0   | 95,158,160  | 182,41,63   |
| <p style="background-color: #7FFF00">　　　</p> | CHARTREUSE                                                   | Chartreuse                                        | #7FFF00   | 127,255,0   | 90,100,100  |
| <p style="background-color: #D2691E">　　　</p> | CHOCOLATE                                                    | Chocolate                                         | #D2691E   | 210,105,30  | 25,86,82    |
| <p style="background-color: #FF7F50">　　　</p> | CORAL                                                        | Coral                                             | #FF7F50   | 255,127,80  | 16,69,100   |
| <p style="background-color: #6495ED">　　　</p> | CORNFLOWER_BLUE                                              | Cornflower Blue                                   | #6495ED   | 100,149,237 | 219,58,93   |
| <p style="background-color: #FFF8DC">　　　</p> | CORN_SILK                                                    | Corn Silk                                         | #FFF8DC   | 255,248,220 | 48,14,100   |
| <p style="background-color: #DC143C">　　　</p> | CRIMSON                                                      | Crimson                                           | #DC143C   | 220,20,60   | 348,91,86   |
| <p style="background-color: #00FFFF">　　　</p> | <span style="white-space:nowrap">CYAN / AQUA</span>          | Cyan / Aqua                                       | #00FFFF   | 0,255,255   | 180,100,100 |
| <p style="background-color: #00008B">　　　</p> | DARK_BLUE                                                    | Dark Blue                                         | #00008B   | 0,0,139     | 240,100,55  |
| <p style="background-color: #008B8B">　　　</p> | DARK_CYAN                                                    | Dark Cyan                                         | #008B8B   | 0,139,139   | 180,100,55  |
| <p style="background-color: #B8860B">　　　</p> | DARK_GOLDENROD                                               | Dark Goldenrod                                    | #B8860B   | 184,134,11  | 43,94,72    |
| <p style="background-color: #A9A9A9">　　　</p> | DARK_GRAY<br/>DARK_GREY                                      | Dark Gray                                         | #A9A9A9   | 169,169,169 | 0,0,66      |
| <p style="background-color: #006400">　　　</p> | DARK_GREEN                                                   | Dark Green                                        | #006400   | 0,100,0     | 120,100,39  |
| <p style="background-color: #BDB76B">　　　</p> | DARK_KHAKI                                                | Dark Khaki                                        | #BDB76B   | 189,183,107 | 56,43,74    |
| <p style="background-color: #8B008B">　　　</p> | DARK_MAGENTA                                              | Dark Magenta                                      | #8B008B   | 139,0,139   | 300,100,55  |
| <p style="background-color: #556B2F">　　　</p> | DARK_OLIVE_GREEN                                          | Dark Olive Green                                  | #556B2F   | 85,107,47   | 82,56,42    |
| <p style="background-color: #FF8C00">　　　</p> | DARK_ORANGE                                               | Dark Orange                                       | #FF8C00   | 255,140,0   | 33,100,100  |
| <p style="background-color: #9932CC">　　　</p> | DARK_ORCHID                                               | Dark Orchid                                       | #9932CC   | 153,50,204  | 280,75,80   |
| <p style="background-color: #8B0000">　　　</p> | DARK_RED                                                  | Dark Red                                          | #8B0000   | 139,0,0     | 0,100,55    |
| <p style="background-color: #E9967A">　　　</p> | DARK_SALMON                                               | Dark Salmon                                       | #E9967A   | 233,150,122 | 15,48,91    |
| <p style="background-color: #8FBC8F">　　　</p> | DARK_SEA_GREEN                                            | Dark Sea Green                                    | #8FBC8F   | 143,188,143 | 120,24,74   |
| <p style="background-color: #483D8B">　　　</p> | DARK_SLATE_BLUE                                           | Dark Slate Blue                                   | #483D8B   | 72,61,139   | 248,56,55   |
| <p style="background-color: #2F4F4F">　　　</p> | DARK_SLATE_GRAY<br/>DARK_SLATE_GREY                       | Dark Slate Gray                                   | #2F4F4F   | 47,79,79    | 180,41,31   |
| <p style="background-color: #00CED1">　　　</p> | DARK_TURQUOISE                                            | Dark Turquoise                                    | #00CED1   | 0,206,209   | 181,100,82  |
| <p style="background-color: #9400D3">　　　</p> | DARK_VIOLET                                               | Dark Violet                                       | #9400D3   | 148,0,211   | 282,100,83  |
| <p style="background-color: #FF1493">　　　</p> | DEEP_PINK                                                 | Deep Pink                                         | #FF1493   | 255,20,147  | 328,92,100  |
| <p style="background-color: #00BFFF">　　　</p> | DEEP_SKY_BLUE                                             | Deep Sky Blue                                     | #00BFFF   | 0,191,255   | 195,100,100 |
| <p style="background-color: #696969">　　　</p> | DIM_GRAY<br/>DIM_GREY                                     | Dim Gray                                          | #696969   | 105,105,105 | 0,0,41      |
| <p style="background-color: #1E90FF">　　　</p> | DODGER_BLUE                                               | Dodger Blue                                       | #1E90FF   | 30,144,255  | 210,88,100  |
| <p style="background-color: #B22222">　　　</p> | FIRE_BRICK                                                | Fire Brick                                        | #B22222   | 178,34,34   | 0,81,70     |
| <p style="background-color: #FFFAF0">　　　</p> | FLORAL_WHITE                                              | Floral White                                      | #FFFAF0   | 255,250,240 | 40,6,100    |
| <p style="background-color: #228B22">　　　</p> | FOREST_GREEN                                              | Forest Green                                      | #228B22   | 34,139,34   | 120,76,55   |
| <p style="background-color: #DCDCDC">　　　</p> | GAINSBORO                                                 | Gainsboro                                         | #DCDCDC   | 220,220,220 | 0,0,86      |
| <p style="background-color: #F8F8FF">　　　</p> | GHOST_WHITE                                               | Ghost White                                       | #F8F8FF   | 248,248,255 | 240,3,100   |
| <p style="background-color: #FFD700">　　　</p> | GOLD                                                      | Gold                                              | #FFD700   | 255,215,0   | 51,100,100  |
| <p style="background-color: #DAA520">　　　</p> | GOLDENROD                                                 | Goldenrod                                         | #DAA520   | 218,165,32  | 43,85,85    |
| <p style="background-color: #808080">　　　</p> | GRAY<br/>GREY                                             | Gray                                              | #808080   | 128,128,128 | 0,0,50      |
| <p style="background-color: #008000">　　　</p> | GREEN                                                     | Green                                             | #008000   | 0,128,0     | 120,100,50  |
| <p style="background-color: #ADFF2F">　　　</p> | GREEN_YELLOW                                              | Green Yellow                                      | #ADFF2F   | 173,255,47  | 84,82,100   |
| <p style="background-color: #F0FFF0">　　　</p> | HONEYDEW                                                  | Honeydew                                          | #F0FFF0   | 240,255,240 | 120,6,100   |
| <p style="background-color: #FF69B4">　　　</p> | HOT_PINK                                                  | Hot Pink                                          | #FF69B4   | 255,105,180 | 330,59,100  |
| <p style="background-color: #CD5C5C">　　　</p> | INDIAN_RED                                                | Indian Red                                        | #CD5C5C   | 205,92,92   | 0,55,80     |
| <p style="background-color: #4B0082">　　　</p> | INDIGO                                                    | Indigo                                            | #4B0082   | 75,0,130    | 275,100,51  |
| <p style="background-color: #FFFFF0">　　　</p> | IVORY                                                     | Ivory                                             | #FFFFF0   | 255,255,240 | 60,6,100    |
| <p style="background-color: #F0E68C">　　　</p> | KHAKI                                                     | Khaki                                             | #F0E68C   | 240,230,140 | 54,42,94    |
| <p style="background-color: #E6E6FA">　　　</p> | LAVENDER                                                  | Lavender                                          | #E6E6FA   | 230,230,250 | 240,8,98    |
| <p style="background-color: #FFF0F5">　　　</p> | LAVENDER_BLUSH                                            | Lavender Blush                                    | #FFF0F5   | 255,240,245 | 340,6,100   |
| <p style="background-color: #7CFC00">　　　</p> | LAWN_GREEN                                                | Lawn Green                                        | #7CFC00   | 124,252,0   | 90,100,99   |
| <p style="background-color: #FFFACD">　　　</p> | LEMON_CHIFFON                                             | Lemon Chiffon                                     | #FFFACD   | 255,250,205 | 54,20,100   |
| <p style="background-color: #ADD8E6">　　　</p> | LIGHT_BLUE                                                | Light Blue                                        | #ADD8E6   | 173,216,230 | 195,25,90   |
| <p style="background-color: #F08080">　　　</p> | LIGHT_CORAL                                               | Light Coral                                       | #F08080   | 240,128,128 | 0,47,94     |
| <p style="background-color: #E0FFFF">　　　</p> | LIGHT_CYAN                                                | Light Cyan                                        | #E0FFFF   | 224,255,255 | 180,12,100  |
| <p style="background-color: #FAFAD2">　　　</p> | LIGHT_GOLDENROD_YELLOW                                    | Light Goldenrod Yellow                            | #FAFAD2   | 250,250,210 | 60,16,98    |
| <p style="background-color: #D3D3D3">　　　</p> | LIGHT_GRAY<br/>LIGHT_GREY                                 | Light Gray                                        | #D3D3D3   | 211,211,211 | 0,0,83      |
| <p style="background-color: #90EE90">　　　</p> | LIGHT_GREEN                                               | Light Green                                       | #90EE90   | 144,238,144 | 120,39,93   |
| <p style="background-color: #FFB6C1">　　　</p> | LIGHT_PINK                                                | Light Pink                                        | #FFB6C1   | 255,182,193 | 351,29,100  |
| <p style="background-color: #FFA07A">　　　</p> | LIGHT_SALMON                                              | Light Salmon                                      | #FFA07A   | 255,160,122 | 17,52,100   |
| <p style="background-color: #20B2AA">　　　</p> | LIGHT_SEA_GREEN                                           | Light Sea Green                                   | #20B2AA   | 32,178,170  | 177,82,70   |
| <p style="background-color: #87CEFA">　　　</p> | LIGHT_SKY_BLUE                                            | Light Sky Blue                                    | #87CEFA   | 135,206,250 | 203,46,98   |
| <p style="background-color: #778899">　　　</p> | LIGHT_SLATE_GRAY<br/>LIGHT_SLATE_GREY                     | Light Slate Gray                                  | #778899   | 119,136,153 | 210,22,60   |
| <p style="background-color: #B0C4DE">　　　</p> | LIGHT_STEEL_BLUE                                          | Light Steel Blue                                  | #B0C4DE   | 176,196,222 | 214,21,87   |
| <p style="background-color: #FFFFE0">　　　</p> | LIGHT_YELLOW                                              | Light Yellow                                      | #FFFFE0   | 255,255,224 | 60,12,100   |
| <p style="background-color: #00FF00">　　　</p> | LIME                                                      | Lime                                              | #00FF00   | 0,255,0     | 120,100,100 |
| <p style="background-color: #32CD32">　　　</p> | LIME_GREEN                                                | Lime Green                                        | #32CD32   | 50,205,50   | 120,76,80   |
| <p style="background-color: #FAF0E6">　　　</p> | LINEN                                                     | Linen                                             | #FAF0E6   | 250,240,230 | 30,8,98     |
| <p style="background-color: #FF00FF">　　　</p> | <span style="white-space:nowrap">MAGENTA / FUCHSIA</span> | Magenta / Fuchsia                                 | #FF00FF   | 255,0,255   | 300,100,100 |
| <p style="background-color: #800000">　　　</p> | MAROON                                                    | Maroon                                            | #800000   | 128,0,0     | 0,100,50    |
| <p style="background-color: #66CDAA">　　　</p> | MEDIUM_AQUAMARINE                                         | Medium Aquamarine                                 | #66CDAA   | 102,205,170 | 160,50,80   |
| <p style="background-color: #0000CD">　　　</p> | MEDIUM_BLUE                                               | Medium Blue                                       | #0000CD   | 0,0,205     | 240,100,80  |
| <p style="background-color: #DDA0DD">　　　</p> | MEDIUM_LAVENDER_MAGENTA                                   | Medium Lavender Magenta                           | #DDA0DD   | 221,160,221 | 300,28,87   |
| <p style="background-color: #BA55D3">　　　</p> | MEDIUM_ORCHID                                             | Medium Orchid                                     | #BA55D3   | 186,85,211  | 288,60,83   |
| <p style="background-color: #9370DB">　　　</p> | MEDIUM_PURPLE                                             | Medium Purple                                     | #9370DB   | 147,112,219 | 260,49,86   |
| <p style="background-color: #3CB371">　　　</p> | MEDIUM_SEA_GREEN                                          | Medium Sea Green                                  | #3CB371   | 60,179,113  | 147,66,70   |
| <p style="background-color: #7B68EE">　　　</p> | MEDIUM_SLATE_BLUE                                         | Medium Slate Blue                                 | #7B68EE   | 123,104,238 | 249,56,93   |
| <p style="background-color: #00FA9A">　　　</p> | MEDIUM_SPRING_GREEN                                       | Medium Spring Green                               | #00FA9A   | 0,250,154   | 157,100,98  |
| <p style="background-color: #48D1CC">　　　</p> | MEDIUM_TURQUOISE                                          | Medium Turquoise                                  | #48D1CC   | 72,209,204  | 178,66,82   |
| <p style="background-color: #C71585">　　　</p> | MEDIUM_VIOLET_RED                                         | Medium Violet Red                                 | #C71585   | 199,21,133  | 322,89,78   |
| <p style="background-color: #191970">　　　</p> | MIDNIGHT_BLUE                                             | Midnight Blue                                     | #191970   | 25,25,112   | 240,78,44   |
| <p style="background-color: #F5FFFA">　　　</p> | MINT_CREAM                                                | Mint Cream                                        | #F5FFFA   | 245,255,250 | 150,4,100   |
| <p style="background-color: #FFE4E1">　　　</p> | MISTY_ROSE                                                | Misty Rose                                        | #FFE4E1   | 255,228,225 | 6,12,100    |
| <p style="background-color: #FFE4B5">　　　</p> | MOCCASIN                                                  | Moccasin                                          | #FFE4B5   | 255,228,181 | 38,29,100   |
| <p style="background-color: #FFDEAD">　　　</p> | NAVAJO_WHITE                                              | Navajo White                                      | #FFDEAD   | 255,222,173 | 36,32,100   |
| <p style="background-color: #000080">　　　</p> | NAVY                                                      | Navy                                              | #000080   | 0,0,128     | 240,100,50  |
| <p style="background-color: #FDF5E6">　　　</p> | OLD_LACE                                                  | Old Lace                                          | #FDF5E6   | 253,245,230 | 39,9,99     |
| <p style="background-color: #808000">　　　</p> | OLIVE                                                     | Olive                                             | #808000   | 128,128,0   | 60,100,50   |
| <p style="background-color: #6B8E23">　　　</p> | OLIVE_DRAB                                                | Olive Drab                                        | #6B8E23   | 107,142,35  | 80,75,56    |
| <p style="background-color: #FFA500">　　　</p> | ORANGE                                                    | Orange                                            | #FFA500   | 255,165,0   | 39,100,100  |
| <p style="background-color: #FF4500">　　　</p> | ORANGE_RED                                                | Orange Red                                        | #FF4500   | 255,69,0    | 16,100,100  |
| <p style="background-color: #DA70D6">　　　</p> | ORCHID                                                    | Orchid                                            | #DA70D6   | 218,112,214 | 302,49,85   |
| <p style="background-color: #EEE8AA">　　　</p> | PALE_GOLDENROD                                            | Pale Goldenrod                                    | #EEE8AA   | 238,232,170 | 55,29,93    |
| <p style="background-color: #98FB98">　　　</p> | PALE_GREEN                                                | Pale Green                                        | #98FB98   | 152,251,152 | 120,39,98   |
| <p style="background-color: #AFEEEE">　　　</p> | PALE_TURQUOISE                                            | Pale Turquoise                                    | #AFEEEE   | 175,238,238 | 180,26,93   |
| <p style="background-color: #DB7093">　　　</p> | PALE_VIOLET_RED                                           | Pale Violet Red                                   | #DB7093   | 219,112,147 | 340,49,86   |
| <p style="background-color: #FFEFD5">　　　</p> | PAPAYA_WHIP                                               | Papaya Whip                                       | #FFEFD5   | 255,239,213 | 37,16,100   |
| <p style="background-color: #800080">　　　</p> | PATRIARCH                                                 | Patriarch                                         | #800080   | 128,0,128   | 300,100,50  |
| <p style="background-color: #FFDAB9">　　　</p> | PEACH_PUFF                                                | Peach Puff                                        | #FFDAB9   | 255,218,185 | 28,27,100   |
| <p style="background-color: #CD853F">　　　</p> | PERU                                                      | Peru                                              | #CD853F   | 205,133,63  | 30,69,80    |
| <p style="background-color: #FFC0CB">　　　</p> | PINK                                                      | <span style="white-space:nowrap">Pink</span>       | #FFC0CB | 255,192,203 | 350,25,100  |
| <p style="background-color: #B0E0E6">　　　</p> | POWDER_BLUE                                               | <span style="white-space:nowrap">Powder Blue</span>       | #B0E0E6 | 176,224,230 | 187,23,90   |
| <p style="background-color: #663399">　　　</p> | REBECCA_PURPLE                                            | <span style="white-space:nowrap">Rebecca Purple</span>     | #663399 | 102,51,153  | 270,67,60   |
| <p style="background-color: #FF0000">　　　</p> | RED                                                       | <span style="white-space:nowrap">Red</span>        | #FF0000 | 255,0,0     | 0,100,100   |
| <p style="background-color: #BC8F8F">　　　</p> | ROSY_BROWN                                                | <span style="white-space:nowrap">Rosy Brown</span>      | #BC8F8F | 188,143,143 | 0,24,74     |
| <p style="background-color: #4169E1">　　　</p> | ROYAL_BLUE                                                | <span style="white-space:nowrap">Royal Blue</span> | #4169E1 | 65,105,225  | 225,71,88   |
| <p style="background-color: #8B4513">　　　</p> | SADDLE_BROWN                                              | <span style="white-space:nowrap">Saddle Brown</span>       | #8B4513 | 139,69,19   | 25,86,55    |
| <p style="background-color: #FA8072">　　　</p> | SALMON                                                    | <span style="white-space:nowrap">Salmon</span>       | #FA8072 | 250,128,114 | 6,54,98     |
| <p style="background-color: #F4A460">　　　</p> | SAND_BROWN                                                | <span style="white-space:nowrap">Sandy Brown</span>       | #F4A460 | 244,164,96  | 28,61,96    |
| <p style="background-color: #FFF5EE">　　　</p> | SEASHELL                                                  | <span style="white-space:nowrap">Seashell</span>       | #FFF5EE | 255,245,238 | 25,7,100    |
| <p style="background-color: #2E8B57">　　　</p> | SEA_GREEN                                                 | <span style="white-space:nowrap">Sea Green</span>       | #2E8B57 | 46,139,87   | 146,67,55   |
| <p style="background-color: #A0522D">　　　</p> | SIENNA                                                    | <span style="white-space:nowrap">Sienna</span>       | #A0522D | 160,82,45   | 19,72,63    |
| <p style="background-color: #C0C0C0">　　　</p> | SILVER                                                    | <span style="white-space:nowrap">Silver</span>        | #C0C0C0 | 192,192,192 | 0,0,75      |
| <p style="background-color: #87CEEB">　　　</p> | SKY_BLUE                                                  | <span style="white-space:nowrap">Sky Blue</span>      | #87CEEB | 135,206,235 | 197,43,92   |
| <p style="background-color: #6A5ACD">　　　</p> | SLATE_BLUE                                                | <span style="white-space:nowrap">Slate Blue</span>       | #6A5ACD | 106,90,205  | 248,56,80   |
| <p style="background-color: #708090">　　　</p> | SLATE_GRAY<br/>SLATE_GREY                                 | <span style="white-space:nowrap">Slate Gray</span>       | #708090 | 112,128,144 | 210,22,56   |
| <p style="background-color: #FFFAFA">　　　</p> | SNOW                                                      | <span style="white-space:nowrap">Snow</span>        | #FFFAFA | 255,250,250 | 0,2,100     |
| <p style="background-color: #00FF7F">　　　</p> | SPRING_GREEN                                              | <span style="white-space:nowrap">Spring Green</span>       | #00FF7F | 0,255,127   | 150,100,100 |
| <p style="background-color: #4682B4">　　　</p> | STEEL_BLUE                                                | <span style="white-space:nowrap">Steel Blue</span>       | #4682B4 | 70,130,180  | 207,61,71   |
| <p style="background-color: #D2B48C">　　　</p> | TAN                                                       | <span style="white-space:nowrap">Tan</span>       | #D2B48C | 210,180,140 | 34,33,82    |
| <p style="background-color: #008080">　　　</p> | TEAL                                                      | <span style="white-space:nowrap">Teal</span>  | #008080 | 0,128,128   | 180,100,50  |
| <p style="background-color: #D8BFD8">　　　</p> | THISTLE                                                   | Thistle                                           | #D8BFD8   | 216,191,216 | 300,12,85   |
| <p style="background-color: #FF6347">　　　</p> | TOMATO                                                    | Tomato                                            | #FF6347   | 255,99,71   | 9,72,100    |
| <p style="background-color: #40E0D0">　　　</p> | TURQUOISE                                                 | Turquoise                                         | #40E0D0   | 64,224,208  | 174,71,88   |
| <p style="background-color: #EE82EE">　　　</p> | VIOLET                                                    | Violet                                            | #EE82EE   | 238,130,238 | 300,45,93   |
| <p style="background-color: #F5DEB3">　　　</p> | WHEAT                                                     | Wheat                                             | #F5DEB3   | 245,222,179 | 39,27,96    |
| <p style="background-color: #FFFFFF">　　　</p> | WHITE                                                     | White                                             | #FFFFFF   | 255,255,255 | 0,0,100     |
| <p style="background-color: #F5F5F5">　　　</p> | WHITE_SMOKE                                               | White Smoke                                       | #F5F5F5   | 245,245,245 | 0,0,96      |
| <p style="background-color: #FFFF00">　　　</p> | YELLOW                                                    | Yellow                                            | #FFFF00   | 255,255,0   | 60,100,100  |
| <p style="background-color: #9ACD32">　　　</p> | YELLOW_GREEN                                              | Yellow Green                                      | #9ACD32   | 154,205,50  | 80,76,80    |

## WEB Color List

This WEB color list combines [X11 color names / CSS3 standard names / HTML4 standard names / SVG color names], etc.

This is a relatively large collection of color lists, but it may not include every single name from the sources above, and new entries may be added from time to time.

Usage:

```js
colors.web.BURNT_ORANGE;
```

> See also: [Wikipedia (EN)](https://en.wikipedia.org/wiki/List_of_colors)

|                      Color                      | Variable Name                                                                | English Name                                                | Hex Code  | RGB         | HSV         |
|:-----------------------------------------------:|------------------------------------------------------------------------------|-------------------------------------------------------------|-----------|-------------|-------------|
| <p style="background-color: #F0F8FF">　　　</p> | ALICE_BLUE                                                                   | Alice Blue                                                  | #F0F8FF   | 240,248,255 | 208,6,100   |
| <p style="background-color: #E32636">　　　</p> | ALIZARIN_CRIMSON                                                             | Alizarin Crimson / Deep Alizarin Crimson                    | #E32636   | 227,38,54   | 355,83,89   |
| <p style="background-color: #FFBF00">　　　</p> | AMBER                                                                        | Amber                                                       | #FFBF00   | 255,191,0   | 45,100,100  |
| <p style="background-color: #9966CC">　　　</p> | AMETHYST                                                                     | Amethyst                                                    | #9966CC   | 153,102,204 | 270,50,80   |
| <p style="background-color: #FAEBD7">　　　</p> | ANTIQUE_WHITE                                                                | Antique White                                               | #FAEBD7   | 250,235,215 | 34,14,98    |
| <p style="background-color: #8CE600">　　　</p> | APPLE_GREEN                                                                  | Apple Green                                                 | #8CE600   | 140,230,0   | 83,100,90   |
| <p style="background-color: #E69966">　　　</p> | APRICOT                                                                      | Apricot                                                     | #E69966   | 230,153,102 | 24,56,90    |
| <p style="background-color: #AFDFE4">　　　</p> | AQUA                                                                         | Aqua                                                        | #AFDFE4   | 175,223,228 | 186,23,89   |
| <p style="background-color: #7FFFD4">　　　</p> | AQUAMARINE                                                                   | Aquamarine                                                  | #7FFFD4   | 127,255,212 | 160,50,100  |
| <p style="background-color: #66FFE6">　　　</p> | AQUA_BLUE                                                                    | Aqua Blue                                                   | #66FFE6   | 102,255,230 | 170,60,100  |
| <p style="background-color: #007FFF">　　　</p> | AZURE                                                                        | Azure                                                       | #007FFF   | 0,127,255   | 210,100,100 |
| <p style="background-color: #89CFF0">　　　</p> | BABY_BLUE                                                                    | Baby Blue                                                   | #89CFF0   | 137,207,240 | 199,43,94   |
| <p style="background-color: #FFD9E6">　　　</p> | BABY_PINK                                                                    | Baby Pink                                                   | #FFD9E6   | 255,217,230 | 339,15,100  |
| <p style="background-color: #F5F5DC">　　　</p> | BEIGE                                                                        | Beige                                                       | #F5F5DC   | 245,245,220 | 60,10,96    |
| <p style="background-color: #FFE4C4">　　　</p> | BISQUE                                                                       | Bisque                                                      | #FFE4C4   | 255,228,196 | 33,23,100   |
| <p style="background-color: #000000">　　　</p> | BLACK                                                                        | Black                                                       | #000000   | 0,0,0       | 0,0,0       |
| <p style="background-color: #FFEBCD">　　　</p> | BLANCHED_ALMOND                                                              | Blanched Almond                                             | #FFEBCD   | 255,235,205 | 36,20,100   |
| <p style="background-color: #0000FF">　　　</p> | BLUE                                                                         | Blue                                                        | #0000FF   | 0,0,255     | 240,100,100 |
| <p style="background-color: #8A2BE2">　　　</p> | BLUE_VIOLET                                                                  | Blue Violet                                                 | #8A2BE2   | 138,43,226  | 271,81,89   |
| <p style="background-color: #66FF00">　　　</p> | BRIGHT_GREEN                                                                 | Bright Green / Vivid Green                                  | #66FF00   | 102,255,0   | 96,100,100  |
| <p style="background-color: #CD7F32">　　　</p> | BRONZE                                                                       | Bronze                                                      | #CD7F32   | 184,115,51  | 29,72,72    |
| <p style="background-color: #A52A2A">　　　</p> | BROWN                                                                        | Brown                                                       | #A52A2A   | 165,42,42   | 0,75,65     |
| <p style="background-color: #800020">　　　</p> | BURGUNDY                                                                     | Burgundy                                                    | #800020   | 128,0,32    | 345,100,50  |
| <p style="background-color: #DEB887">　　　</p> | BURLY_WOOD                                                                   | Burly Wood                                                  | #DEB887   | 222,184,135 | 34,39,87    |
| <p style="background-color: #CC5500">　　　</p> | BURNT_ORANGE                                                       | Burnt Orange                                      | #CC5500   | 204,85,0    | 25,100,80   |
| <p style="background-color: #5F9EA0">　　　</p> | CADET_BLUE                                                         | Cadet Blue                                        | #5F9EA0   | 95,158,160  | 182,41,63   |
| <p style="background-color: #A16B47">　　　</p> | CAMEL                                                              | Camel                                             | #A16B47   | 161,107,71  | 24,56,63    |
| <p style="background-color: #E63995">　　　</p> | CAMELLIA                                                           | Camellia                                          | #E63995   | 230,57,149  | 328,75,90   |
| <p style="background-color: #FFEF00">　　　</p> | CANARY_YELLOW                                                      | Canary Yellow                                     | #FFEF00   | 255,239,0   | 56,100,100  |
| <p style="background-color: #990036">　　　</p> | CARDINAL_RED                                                       | Cardinal Red                                      | #990036   | 153,0,54    | 339,100,60  |
| <p style="background-color: #E6005C">　　　</p> | CARMINE                                                            | Carmine                                           | #E6005C   | 230,0,92    | 336,100,90  |
| <p style="background-color: #ACE1AF">　　　</p> | CELADON                                                            | Celadon                                           | #ACE1AF   | 172,225,175 | 123,24,88   |
| <p style="background-color: #DE3163">　　　</p> | CERISE                                                             | Cerise                                            | #DE3163   | 222,49,99   | 343,78,87   |
| <p style="background-color: #2A52BE">　　　</p> | CERULEAN_BLUE                                                      | Cerulean Blue                                     | #2A52BE   | 42,82,190   | 224,78,75   |
| <p style="background-color: #FFFF99">　　　</p> | CHAMPAGNE_YELLOW                                                   | Champagne Yellow                                  | #FFFF99   | 255,255,153 | 60,40,100   |
| <p style="background-color: #7FFF00">　　　</p> | CHARTREUSE                                                         | Chartreuse                                        | #7FFF00   | 127,255,0   | 90,100,100  |
| <p style="background-color: #D2691E">　　　</p> | CHOCOLATE                                                          | Chocolate                                         | #D2691E   | 210,105,30  | 25,86,82    |
| <p style="background-color: #E6B800">　　　</p> | CHROME_YELLOW                                                      | Chrome Yellow                                     | #E6B800   | 230,184,0   | 48,100,90   |
| <p style="background-color: #CCA3CC">　　　</p> | CLEMATIS                                                           | Clematis                                          | #CCA3CC   | 204,163,204 | 300,20,80   |
| <p style="background-color: #0047AB">　　　</p> | COBALT_BLUE                                                        | Cobalt Blue                                       | #0047AB   | 0,71,171    | 215,100,67  |
| <p style="background-color: #66FF59">　　　</p> | COBALT_GREEN                                                       | Cobalt Green                                      | #66FF59   | 102,255,89  | 115,65,100  |
| <p style="background-color: #4D1F00">　　　</p> | COCONUT_BROWN                                                      | Coconut Brown                                     | #4D1F00   | 77,31,0     | 24,100,30   |
| <p style="background-color: #4D3900">　　　</p> | COFFEE                                                             | Coffee                                            | #4D3900   | 77,57,0     | 44,100,30   |
| <p style="background-color: #FF7F50">　　　</p> | CORAL                                                              | Coral                                             | #FF7F50   | 255,127,80  | 16,69,100   |
| <p style="background-color: #FF80BF">　　　</p> | CORAL_PINK                                                         | Coral Pink                                        | #FF80BF   | 255,128,191 | 330,50,100  |
| <p style="background-color: #6495ED">　　　</p> | CORNFLOWER_BLUE                                                    | Cornflower Blue                                   | #6495ED   | 100,149,237 | 219,58,93   |
| <p style="background-color: #FFF8DC">　　　</p> | CORN_SILK                                                          | Corn Silk                                         | #FFF8DC   | 255,248,220 | 48,14,100   |
| <p style="background-color: #FFFDD0">　　　</p> | CREAM                                                              | Cream                                             | #FFFDD0   | 255,253,208 | 57,18,100   |
| <p style="background-color: #DC143C">　　　</p> | CRIMSON                                                            | Crimson                                           | #DC143C   | 220,20,60   | 348,91,86   |
| <p style="background-color: #00FFFF">　　　</p> | CYAN                                                               | Cyan                                              | #00FFFF   | 0,255,255   | 180,100,100 |
| <p style="background-color: #0DBF8C">　　　</p> | CYAN_BLUE                                                          | Cyan Blue                                         | #0DBF8C   | 13,191,140  | 163,93,75   |
| <p style="background-color: #00008B">　　　</p> | DARK_BLUE                                                          | Dark Blue                                         | #00008B   | 0,0,139     | 240,100,55  |
| <p style="background-color: #008B8B">　　　</p> | DARK_CYAN                                                          | Dark Cyan                                         | #008B8B   | 0,139,139   | 180,100,55  |
| <p style="background-color: #B8860B">　　　</p> | DARK_GOLDENROD                                                     | Dark Goldenrod                                    | #B8860B   | 184,134,11  | 43,94,72    |
| <p style="background-color: #A9A9A9">　　　</p> | DARK_GRAY                                                          | Dark Gray                                         | #A9A9A9   | 169,169,169 | 0,0,66      |
| <p style="background-color: #006400">　　　</p> | DARK_GREEN                                                         | Dark Green                                        | #006400   | 0,100,0     | 120,100,39  |
| <p style="background-color: #BDB76B">　　　</p> | DARK_KHAKI                                                         | Dark Khaki                                        | #BDB76B   | 189,183,107 | 56,43,74    |
| <p style="background-color: #8B008B">　　　</p> | DARK_MAGENTA                                                       | Dark Magenta                                      | #8B008B   | 139,0,139   | 300,100,55  |
| <p style="background-color: #24367D">　　　</p> | DARK_MINERAL_BLUE                                                  | Dark Mineral Blue                                 | #24367D   | 36,54,125   | 228,71,49   |
| <p style="background-color: #556B2F">　　　</p> | DARK_OLIVE_GREEN                                                   | Dark Olive Green                                  | #556B2F   | 85,107,47   | 82,56,42    |
| <p style="background-color: #FF8C00">　　　</p> | DARK_ORANGE                                                        | Dark Orange                                       | #FF8C00   | 255,140,0   | 33,100,100  |
| <p style="background-color: #9932CC">　　　</p> | DARK_ORCHID                                                        | Dark Orchid                                       | #9932CC   | 153,50,204  | 280,75,80   |
| <p style="background-color: #003399">　　　</p> | DARK_POWDER_BLUE                                                   | Dark Powder Blue                                  | #003399   | 0,51,153    | 220,100,60  |
| <p style="background-color: #8B0000">　　　</p> | DARK_RED                                                           | Dark Red                                          | #8B0000   | 139,0,0     | 0,100,55    |
| <p style="background-color: #E9967A">　　　</p> | DARK_SALMON                                                        | Dark Salmon                                       | #E9967A   | 233,150,122 | 15,48,91    |
| <p style="background-color: #8FBC8F">　　　</p> | DARK_SEA_GREEN                                                     | Dark Sea Green                                    | #8FBC8F   | 143,188,143 | 120,24,74   |
| <p style="background-color: #483D8B">　　　</p> | DARK_SLATE_BLUE                                                    | Dark Slate Blue                                   | #483D8B   | 72,61,139   | 248,56,55   |
| <p style="background-color: #2F4F4F">　　　</p> | DARK_SLATE_GRAY                                                    | Dark Slate Gray                                   | #2F4F4F   | 47,79,79    | 180,41,31   |
| <p style="background-color: #00CED1">　　　</p> | DARK_TURQUOISE                                                     | Dark Turquoise                                    | #00CED1   | 0,206,209   | 181,100,82  |
| <p style="background-color: #9400D3">　　　</p> | DARK_VIOLET                                                        | <span style="white-space:nowrap">Dark Violet</span>          | #9400D3 | 148,0,211   | 282,100,83  |
| <p style="background-color: #FF1493">　　　</p> | DEEP_PINK                                                          | <span style="white-space:nowrap">Deep Pink</span>         | #FF1493 | 255,20,147  | 328,92,100  |
| <p style="background-color: #00BFFF">　　　</p> | DEEP_SKY_BLUE                                                      | <span style="white-space:nowrap">Deep Sky Blue</span>         | #00BFFF | 0,191,255   | 195,100,100 |
| <p style="background-color: #696969">　　　</p> | DIM_GRAY                                                           | <span style="white-space:nowrap">Dim Gray</span>          | #696969 | 105,105,105 | 0,0,41      |
| <p style="background-color: #1E90FF">　　　</p> | DODGER_BLUE                                                        | <span style="white-space:nowrap">Dodger Blue</span>         | #1E90FF | 30,144,255  | 210,88,100  |
| <p style="background-color: #50C878">　　　</p> | EMERALD                                                            | <span style="white-space:nowrap">Emerald</span>          | #50C878 | 80,200,120  | 140,60,78   |
| <p style="background-color: #B22222">　　　</p> | FIRE_BRICK                                                         | <span style="white-space:nowrap">Fire Brick</span>          | #B22222 | 178,34,34   | 0,81,70     |
| <p style="background-color: #E68AB8">　　　</p> | FLAMINGO                                                           | <span style="white-space:nowrap">Flamingo</span>         | #E68AB8 | 230,138,184 | 330,40,90   |
| <p style="background-color: #FFFAF0">　　　</p> | FLORAL_WHITE                                                       | <span style="white-space:nowrap">Floral White</span>         | #FFFAF0 | 255,250,240 | 40,6,100    |
| <p style="background-color: #73B839">　　　</p> | FOLIAGE_GREEN                                                      | <span style="white-space:nowrap">Foliage Green</span>          | #73B839 | 115,184,57  | 93,69,72    |
| <p style="background-color: #228B22">　　　</p> | FOREST_GREEN                                                       | <span style="white-space:nowrap">Forest Green</span>         | #228B22 | 34,139,34   | 120,76,55   |
| <p style="background-color: #99FF4D">　　　</p> | FRESH_LEAVES                                                       | <span style="white-space:nowrap">Fresh Green</span>          | #99FF4D | 153,255,77  | 94,70,100   |
| <p style="background-color: #F400A1">　　　</p> | FUCHSIA                                                            | <span style="white-space:nowrap">Fuchsia / Magenta Red</span>          | #F400A1 | 244,0,161   | 320,100,96  |
| <p style="background-color: #DCDCDC">　　　</p> | GAINSBORO                                                          | <span style="white-space:nowrap">Gainsboro Gray</span>       | #DCDCDC | 220,220,220 | 0,0,86      |
| <p style="background-color: #F8F8FF">　　　</p> | GHOST_WHITE                                                        | <span style="white-space:nowrap">Ghost White</span>         | #F8F8FF | 248,248,255 | 240,3,100   |
| <p style="background-color: #FFD700">　　　</p> | <span style="white-space:nowrap">GOLDEN / GOLD</span>              | <span style="white-space:nowrap">Gold</span>           | #FFD700 | 255,215,0   | 51,100,100  |
| <p style="background-color: #DAA520">　　　</p> | GOLDENROD                                                          | <span style="white-space:nowrap">Goldenrod</span>          | #DAA520 | 218,165,32  | 43,85,85    |
| <p style="background-color: #99E64D">　　　</p> | GRASS_GREEN                                                        | <span style="white-space:nowrap">Grass Green</span>          | #99E64D | 153,230,77  | 90,67,90    |
| <p style="background-color: #808080">　　　</p> | GRAY                                                               | <span style="white-space:nowrap">Gray</span>           | #808080 | 128,128,128 | 0,0,50      |
| <p style="background-color: #8674A1">　　　</p> | GRAYISH_PURPLE                                                     | <span style="white-space:nowrap">Grayish Purple</span>         | #8674A1 | 134,116,161 | 264,28,63   |
| <p style="background-color: #008000">　　　</p> | GREEN                                                              | <span style="white-space:nowrap">Green</span>           | #008000 | 0,128,0     | 120,100,50  |
| <p style="background-color: #ADFF2F">　　　</p> | GREEN_YELLOW                                                       | <span style="white-space:nowrap">Green Yellow</span>          | #ADFF2F | 173,255,47  | 84,82,100   |
| <p style="background-color: #DF73FF">　　　</p> | HELIOTROPE                                                         | <span style="white-space:nowrap">Heliotrope</span>         | #DF73FF | 223,115,255 | 286,55,100  |
| <p style="background-color: #F0FFF0">　　　</p> | HONEYDEW                                                           | <span style="white-space:nowrap">Honeydew</span>         | #F0FFF0 | 240,255,240 | 120,6,100   |
| <p style="background-color: #FFB366">　　　</p> | HONEY_ORANGE                                                       | <span style="white-space:nowrap">Honey Orange</span>          | #FFB366 | 255,179,102 | 30,60,100   |
| <p style="background-color: #B8DDC8">　　　</p> | HORIZON_BLUE                                                       | <span style="white-space:nowrap">Horizon Blue</span>           | #B8DDC8 | 184,221,200 | 146,35,100  |
| <p style="background-color: #FF69B4">　　　</p> | HOT_PINK                                                           | <span style="white-space:nowrap">Hot Pink</span>         | #FF69B4 | 255,105,180 | 330,59,100  |
| <p style="background-color: #CD5C5C">　　　</p> | INDIAN_RED                                                         | <span style="white-space:nowrap">Indian Red</span>         | #CD5C5C | 205,92,92   | 0,55,80     |
| <p style="background-color: #4B0080">　　　</p> | INDIGO                                                             | <span style="white-space:nowrap">Indigo</span>           | #4B0080 | 75,0,128    | 275,100,50  |
| <p style="background-color: #002FA7">　　　</p> | INTERNATIONAL_KLEIN_BLUE                                           | <span style="white-space:nowrap">International Klein Blue</span>       | #002FA7 | 0,47,167    | 223,100,65  |
| <p style="background-color: #625B57">　　　</p> | IRON_GRAY                                                          | <span style="white-space:nowrap">Iron Gray</span>          | #625B57 | 98,91,87    | 21,12,39    |
| <p style="background-color: #FFFFF0">　　　</p> | IVORY                                                              | <span style="white-space:nowrap">Ivory</span>          | #FFFFF0 | 255,255,240 | 60,6,100    |
| <p style="background-color: #36BF36">　　　</p> | IVY_GREEN                                                          | <span style="white-space:nowrap">Ivy Green</span>        | #36BF36 | 54,191,54   | 120,72,75   |
| <p style="background-color: #E6C35C">　　　</p> | JASMINE                                                            | <span style="white-space:nowrap">Jasmine</span>         | #E6C35C | 230,195,92  | 45,60,90    |
| <p style="background-color: #996B1F">　　　</p> | KHAKI                                                              | <span style="white-space:nowrap">Khaki</span>          | #996B1F | 153,107,31  | 37,80,60    |
| <p style="background-color: #26619C">　　　</p> | LAPIS_LAZULI                                                       | <span style="white-space:nowrap">Lapis Lazuli</span>        | #26619C | 38,97,156   | 210,76,61   |
| <p style="background-color: #B57EDC">　　　</p> | LAVENDER                                                           | <span style="white-space:nowrap">Lavender</span>        | #B57EDC | 181,126,220 | 275,43,86   |
| <p style="background-color: #CCCCFF">　　　</p> | <span style="white-space:nowrap">LAVENDER_BLUE / PERIWINKLE</span> | <span style="white-space:nowrap">Lavender Blue / Periwinkle</span>  | #CCCCFF | 204,204,255 | 240,20,100  |
| <p style="background-color: #FFF0F5">　　　</p> | LAVENDER_BLUSH                                                     | <span style="white-space:nowrap">Lavender Blush</span>       | #FFF0F5 | 255,240,245 | 340,6,100   |
| <p style="background-color: #EE82EE">　　　</p> | LAVENDER_MAGENTA                                                   | <span style="white-space:nowrap">Lavender Magenta</span>          | #EE82EE | 238,130,238 | 300,45,93   |
| <p style="background-color: #E6E6FA">　　　</p> | LAVENDER_MIST                                                      | <span style="white-space:nowrap">Lavender Mist</span>        | #E6E6FA | 230,230,250 | 240,8,98    |
| <p style="background-color: #7CFC00">　　　</p> | LAWN_GREEN                                                         | <span style="white-space:nowrap">Lawn Green</span>         | #7CFC00 | 124,252,0   | 90,100,99   |
| <p style="background-color: #FFFACD">　　　</p> | LEMON_CHIFFON                                                      | <span style="white-space:nowrap">Lemon Chiffon</span>         | #FFFACD | 255,250,205 | 54,20,100   |
| <p style="background-color: #ADD8E6">　　　</p> | LIGHT_BLUE                                                         | <span style="white-space:nowrap">Light Blue</span>          | #ADD8E6 | 173,216,230 | 195,25,90   |
| <p style="background-color: #F08080">　　　</p> | LIGHT_CORAL                                                        | <span style="white-space:nowrap">Light Coral</span>         | #F08080 | 240,128,128 | 0,47,94     |
| <p style="background-color: #E0FFFF">　　　</p> | LIGHT_CYAN                                                         | <span style="white-space:nowrap">Light Cyan</span>          | #E0FFFF | 224,255,255 | 180,12,100  |
| <p style="background-color: #FAFAD2">　　　</p> | LIGHT_GOLDENROD_YELLOW                                             | <span style="white-space:nowrap">Light Goldenrod Yellow</span>        | #FAFAD2 | 250,250,210 | 60,16,98    |
| <p style="background-color: #D3D3D3">　　　</p> | LIGHT_GRAY                                                         | <span style="white-space:nowrap">Light Gray</span>          | #D3D3D3 | 211,211,211 | 0,0,83      |
| <p style="background-color: #90EE90">　　　</p> | LIGHT_GREEN                                                        | <span style="white-space:nowrap">Light Green</span>          | #90EE90 | 144,238,144 | 120,39,93   |
| <p style="background-color: #F0E68C">　　　</p> | LIGHT_KHAKI                                                        | <span style="white-space:nowrap">Light Khaki</span>         | #F0E68C | 240,230,140 | 54,42,94    |
| <p style="background-color: #FFB6C1">　　　</p> | LIGHT_PINK                                                         | <span style="white-space:nowrap">Light Pink</span>         | #FFB6C1 | 255,182,193 | 351,29,100  |
| <p style="background-color: #FFA07A">　　　</p> | LIGHT_SALMON                                                       | <span style="white-space:nowrap">Light Salmon</span>         | #FFA07A | 255,160,122 | 17,52,100   |
| <p style="background-color: #20B2AA">　　　</p> | LIGHT_SEA_GREEN                                                    | <span style="white-space:nowrap">Light Sea Green</span>         | #20B2AA | 32,178,170  | 177,82,70   |
| <p style="background-color: #87CEFA">　　　</p> | LIGHT_SKY_BLUE                                                     | <span style="white-space:nowrap">Light Sky Blue</span>         | #87CEFA | 135,206,250 | 203,46,98   |
| <p style="background-color: #778899">　　　</p> | LIGHT_SLATE_GRAY                                                   | <span style="white-space:nowrap">Light Slate Gray</span>         | #778899 | 119,136,153 | 210,22,60   |
| <p style="background-color: #B0C4DE">　　　</p> | LIGHT_STEEL_BLUE                                                   | <span style="white-space:nowrap">Light Steel Blue</span>         | #B0C4DE | 176,196,222 | 214,21,87   |
| <p style="background-color: #B09DB9">　　　</p> | LIGHT_VIOLET                                                       | <span style="white-space:nowrap">Lavender Magenta</span>          | #B09DB9 | 176,157,185 | 281,15,73   |
| <p style="background-color: #FFFFE0">　　　</p> | LIGHT_YELLOW                                                       | <span style="white-space:nowrap">Light Yellow</span>          | #FFFFE0 | 255,255,224 | 60,12,100   |
| <p style="background-color: #C8A2C8">　　　</p> | LILAC                                                              | <span style="white-space:nowrap">Lilac</span>         | #C8A2C8 | 200,162,200 | 300,19,78   |
| <p style="background-color: #CCFF00">　　　</p> | <span style="white-space:nowrap">LIME / LIGHT_LIME</span>          | <span style="white-space:nowrap">Lime / Light Lime</span>  | #CCFF00 | 204,255,0   | 72,100,100  |
| <p style="background-color: #32CD32">　　　</p> | LIME_GREEN                                                         | <span style="white-space:nowrap">Lime Green</span>         | #32CD32 | 50,205,50   | 120,76,80   |
| <p style="background-color: #FAF0E6">　　　</p> | LINEN                                                              | <span style="white-space:nowrap">Linen</span>          | #FAF0E6 | 250,240,230 | 30,8,98     |
| <p style="background-color: #FF00FF">　　　</p> | MAGENTA                                                            | <span style="white-space:nowrap">Magenta / Fuchsia</span>     | #FF00FF | 255,0,255   | 300,100,100 |
| <p style="background-color: #FF0DA6">　　　</p> | MAGENTA_ROSE                                                       | <span style="white-space:nowrap">Magenta Rose</span>        | #FF0DA6 | 255,13,166  | 322,95,100  |
| <p style="background-color: #22C32E">　　　</p> | MALACHITE                                                          | <span style="white-space:nowrap">Malachite</span>        | #22C32E | 34,195,46   | 124,83,76   |
| <p style="background-color: #D94DFF">　　　</p> | MALLOW                                                             | <span style="white-space:nowrap">Mallow</span>         | #D94DFF | 217,77,255  | 287,70,100  |
| <p style="background-color: #FF9900">　　　</p> | MARIGOLD                                                           | <span style="white-space:nowrap">Marigold</span>        | #FF9900 | 255,153,0   | 36,100,100  |
| <p style="background-color: #00477D">　　　</p> | MARINE_BLUE                                                        | <span style="white-space:nowrap">Marine Blue</span>         | #00477D | 0,71,125    | 206,100,49  |
| <p style="background-color: #800000">　　　</p> | MAROON                                                             | <span style="white-space:nowrap">Maroon</span>           | #800000 | 128,0,0     | 0,100,50    |
| <p style="background-color: #E0B0FF">　　　</p> | MAUVE                                                              | <span style="white-space:nowrap">Mauve</span>         | #E0B0FF | 224,176,255 | 276,31,100  |
| <p style="background-color: #66CDAA">　　　</p> | MEDIUM_AQUAMARINE                                                  | <span style="white-space:nowrap">Medium Aquamarine</span>         | #66CDAA | 102,205,170 | 160,50,80   |
| <p style="background-color: #0000CD">　　　</p> | MEDIUM_BLUE                                                        | <span style="white-space:nowrap">Medium Blue</span>          | #0000CD | 0,0,205     | 240,100,80  |
| <p style="background-color: #DDA0DD">　　　</p> | MEDIUM_LAVENDER_MAGENTA                                            | <span style="white-space:nowrap">Medium Lavender Magenta</span>          | #DDA0DD | 221,160,221 | 300,28,87   |
| <p style="background-color: #BA55D3">　　　</p> | MEDIUM_ORCHID                                                      | <span style="white-space:nowrap">Medium Orchid</span>         | #BA55D3 | 186,85,211  | 288,60,83   |
| <p style="background-color: #9370DB">　　　</p> | MEDIUM_PURPLE                                                      | <span style="white-space:nowrap">Medium Purple</span>          | #9370DB | 147,112,219 | 260,49,86   |
| <p style="background-color: #3CB371">　　　</p> | MEDIUM_SEA_GREEN                                                   | <span style="white-space:nowrap">Medium Sea Green</span>         | #3CB371 | 60,179,113  | 147,66,70   |
| <p style="background-color: #7B68EE">　　　</p> | MEDIUM_SLATE_BLUE                                                  | <span style="white-space:nowrap">Medium Slate Blue</span>         | #7B68EE | 123,104,238 | 249,56,93   |
| <p style="background-color: #00FA9A">　　　</p> | MEDIUM_SPRING_GREEN                                                | <span style="white-space:nowrap">Medium Spring Green</span>         | #00FA9A | 0,250,154   | 157,100,98  |
| <p style="background-color: #48D1CC">　　　</p> | MEDIUM_TURQUOISE                                                   | <span style="white-space:nowrap">Medium Turquoise</span>        | #48D1CC | 72,209,204  | 178,66,82   |
| <p style="background-color: #C71585">　　　</p> | MEDIUM_VIOLET_RED                                                  | <span style="white-space:nowrap">Medium Violet Red</span>        | #C71585 | 199,21,133  | 322,89,78   |
| <p style="background-color: #191970">　　　</p> | MIDNIGHT_BLUE                                                      | <span style="white-space:nowrap">Midnight Blue</span>         | #191970 | 25,25,112   | 240,78,44   |
| <p style="background-color: #E6D933">　　　</p> | MIMOSA                                                             | <span style="white-space:nowrap">Mimosa Yellow</span>        | #E6D933 | 230,217,51  | 56,78,90    |
| <p style="background-color: #004D99">　　　</p> | MINERAL_BLUE                                                       | <span style="white-space:nowrap">Mineral Blue</span>          | #004D99 | 0,77,153    | 210,100,60  |
| <p style="background-color: #A39DAE">　　　</p> | MINERAL_VIOLET                                                     | <span style="white-space:nowrap">Mineral Violet</span>          | #A39DAE | 163,157,174 | 261,10,68   |
| <p style="background-color: #16982B">　　　</p> | MINT                                                               | <span style="white-space:nowrap">Mint Green</span>         | #16982B | 22,152,43   | 130,86,60   |
| <p style="background-color: #F5FFFA">　　　</p> | MINT_CREAM                                                         | <span style="white-space:nowrap">Mint Cream</span>        | #F5FFFA | 245,255,250 | 150,4,100   |
| <p style="background-color: #FFE4E1">　　　</p> | MISTY_ROSE                                                         | <span style="white-space:nowrap">Misty Rose</span>         | #FFE4E1 | 255,228,225 | 6,12,100    |
| <p style="background-color: #FFE4B5">　　　</p> | MOCCASIN                                                           | <span style="white-space:nowrap">Moccasin</span>         | #FFE4B5 | 255,228,181 | 38,29,100   |
| <p style="background-color: #FFFF4D">　　　</p> | MOON_YELLOW                                                        | <span style="white-space:nowrap">Moon Yellow</span>          | #FFFF4D | 255,255,77  | 60,70,100   |
| <p style="background-color: #697723">　　　</p> | MOSS_GREEN                                                         | <span style="white-space:nowrap">Moss Green</span>         | #697723 | 105,119,35  | 70,71,47    |
| <p style="background-color: #CCCC4D">　　　</p> | MUSTARD                                                            | <span style="white-space:nowrap">Mustard</span>         | #CCCC4D | 204,204,77  | 60,62,80    |
| <p style="background-color: #FFDEAD">　　　</p> | NAVAJO_WHITE                                                       | <span style="white-space:nowrap">Navajo White</span>        | #FFDEAD | 255,222,173 | 36,32,100   |
| <p style="background-color: #000080">　　　</p> | <span style="white-space:nowrap">NAVY / NAVY_BLUE</span>           | <span style="white-space:nowrap">Navy / Navy Blue</span>    | #000080 | 0,0,128     | 240,100,50  |
| <p style="background-color: #CC7722">　　　</p> | OCHER                                                              | <span style="white-space:nowrap">Ocher</span>           | #CC7722 | 204,119,34  | 30,83,80    |
| <p style="background-color: #FDF5E6">　　　</p> | OLD_LACE                                                           | <span style="white-space:nowrap">Old Lace</span>         | #FDF5E6 | 253,245,230 | 39,9,99     |
| <p style="background-color: #C08081">　　　</p> | OLD_ROSE                                                           | <span style="white-space:nowrap">Old Rose</span>         | #C08081 | 192,128,129 | 359,33,75   |
| <p style="background-color: #808000">　　　</p> | OLIVE                                                              | <span style="white-space:nowrap">Olive</span>          | #808000 | 128,128,0   | 60,100,50   |
| <p style="background-color: #6B8E23">　　　</p> | OLIVE_DRAB                                                         | <span style="white-space:nowrap">Olive Drab</span>       | #6B8E23 | 107,142,35  | 80,75,56    |
| <p style="background-color: #B784A7">　　　</p> | OPERA_MAUVE                                                        | <span style="white-space:nowrap">Opera Mauve</span>        | #B784A7 | 183,132,167 | 319,28,72   |
| <p style="background-color: #FFA500">　　　</p> | ORANGE                                                             | <span style="white-space:nowrap">Orange</span>           | #FFA500 | 255,165,0   | 39,100,100  |
| <p style="background-color: #FF4500">　　　</p> | ORANGE_RED                                                         | <span style="white-space:nowrap">Orange Red</span>          | #FF4500 | 255,69,0    | 16,100,100  |
| <p style="background-color: #DA70D6">　　　</p> | ORCHID                                                             | <span style="white-space:nowrap">Orchid</span>     | #DA70D6 | 218,112,214 | 302,49,85   |
| <p style="background-color: #E6CFE6">　　　</p> | PAIL_LILAC                                                         | <span style="white-space:nowrap">Pail Lilac</span>        | #E6CFE6 | 230,207,230 | 300,10,90   |
| <p style="background-color: #D1EDF2">　　　</p> | PALE_BLUE                                                          | <span style="white-space:nowrap">Pale Blue</span>          | #D1EDF2 | 209,237,242 | 189,14,95   |
| <p style="background-color: #5E86C1">　　　</p> | PALE_DENIM                                                         | <span style="white-space:nowrap">Pale Denim</span> | #5E86C1 | 94,134,193  | 216,51,76   |
| <p style="background-color: #EEE8AA">　　　</p> | PALE_GOLDENROD                                                     | <span style="white-space:nowrap">Pale Goldenrod</span>         | #EEE8AA | 238,232,170 | 55,29,93    |
| <p style="background-color: #98FB98">　　　</p> | PALE_GREEN                                                         | <span style="white-space:nowrap">Pale Green</span>          | #98FB98 | 152,251,152 | 120,39,98   |
| <p style="background-color: #CCB38C">　　　</p> | PALE_OCHRE                                                         | <span style="white-space:nowrap">Pale Ochre</span>          | #CCB38C | 204,179,140 | 37,31,80    |
| <p style="background-color: #AFEEEE">　　　</p> | PALE_TURQUOISE                                                     | <span style="white-space:nowrap">Pale Turquoise</span>        | #AFEEEE | 175,238,238 | 180,26,93   |
| <p style="background-color: #DB7093">　　　</p> | PALE_VIOLET_RED                                                    | <span style="white-space:nowrap">Pale Violet Red</span>         | #DB7093 | 219,112,147 | 340,49,86   |
| <p style="background-color: #7400A1">　　　</p> | PANSY                                                              | <span style="white-space:nowrap">Pansy</span>        | #7400A1 | 116,0,161   | 283,100,63  |
| <p style="background-color: #FFEFD5">　　　</p> | PAPAYA_WHIP                                                        | <span style="white-space:nowrap">Papaya Whip</span>         | #FFEFD5 | 255,239,213 | 37,16,100   |
| <p style="background-color: #800080">　　　</p> | PATRIARCH                                                          | <span style="white-space:nowrap">Patriarch</span>         | #800080 | 128,0,128   | 300,100,50  |
| <p style="background-color: #FFE5B4">　　　</p> | PEACH                                                              | <span style="white-space:nowrap">Peach</span>           | #FFE5B4 | 255,229,180 | 39,29,100   |
| <p style="background-color: #FBBEA1">　　　</p> | PEACH_PEARL                                                        | <span style="white-space:nowrap">Peach Pearl</span>         | #FBBEA1 | 251,190,161 | 40,29,100   |
| <p style="background-color: #FFDAB9">　　　</p> | PEACH_PUFF                                                         | <span style="white-space:nowrap">Peach Puff</span>         | #FFDAB9 | 255,218,185 | 28,27,100   |
| <p style="background-color: #00808C">　　　</p> | PEACOCK_BLUE                                                       | <span style="white-space:nowrap">Peacock Blue</span>         | #00808C | 0,128,140   | 185,100,55  |
| <p style="background-color: #00A15C">　　　</p> | PEACOCK_GREEN                                                      | <span style="white-space:nowrap">Peacock Green</span>         | #00A15C | 0,161,92    | 154,100,63  |
| <p style="background-color: #FFB3E6">　　　</p> | PEARL_PINK                                                         | <span style="white-space:nowrap">Pearl Pink</span>        | #FFB3E6 | 255,179,230 | 320,30,100  |
| <p style="background-color: #FF4D40">　　　</p> | PERSIMMON                                                          | <span style="white-space:nowrap">Persimmon</span>         | #FF4D40 | 255,77,64   | 4,75,100    |
| <p style="background-color: #CD853F">　　　</p> | PERU                                                               | <span style="white-space:nowrap">Peru</span>          | #CD853F | 205,133,63  | 30,69,80    |
| <p style="background-color: #FFC0CB">　　　</p> | PINK                                                               | <span style="white-space:nowrap">Pink</span>          | #FFC0CB | 255,192,203 | 350,25,100  |
| <p style="background-color: #8E4585">　　　</p> | PLUM                                                               | <span style="white-space:nowrap">Medium Lavender Magenta</span>          | #8E4585 | 142,69,133  | 307,51,56   |
| <p style="background-color: #B0E0E6">　　　</p> | POWDER_BLUE                                                        | <span style="white-space:nowrap">Powder Blue</span>          | #B0E0E6 | 176,224,230 | 187,23,90   |
| <p style="background-color: #003153">　　　</p> | PRUSSIAN_BLUE                                                      | <span style="white-space:nowrap">Prussian Blue</span>        | #003153 | 0,49,83     | 205,100,43  |
| <p style="background-color: #6A0DAD">　　　</p> | PURPLE                                                             | <span style="white-space:nowrap">Purple</span>           | #6A0DAD | 106,13,173  | 275,92,68   |
| <p style="background-color: #FF0000">　　　</p> | RED                                                                | <span style="white-space:nowrap">Red</span>           | #FF0000 | 255,0,0     | 0,100,100   |
| <p style="background-color: #FF007F">　　　</p> | ROSE                                                               | <span style="white-space:nowrap">Rose</span>         | #FF007F | 255,0,127   | 330,100,100 |
| <p style="background-color: #FF66CC">　　　</p> | ROSE_PINK                                                          | <span style="white-space:nowrap">Rose Pink</span>        | #FF66CC | 255,102,204 | 320,60,100  |
| <p style="background-color: #BC8F8F">　　　</p> | ROSY_BROWN                                                         | <span style="white-space:nowrap">Rosy Brown</span>         | #BC8F8F | 188,143,143 | 0,24,74     |
| <p style="background-color: #4169E1">　　　</p> | ROYAL_BLUE                                                         | <span style="white-space:nowrap">Royal Blue</span>    | #4169E1 | 65,105,225  | 225,71,88   |
| <p style="background-color: #CC0080">　　　</p> | RUBY                                                               | <span style="white-space:nowrap">Ruby</span>         | #CC0080 | 204,0,128   | 322,100,80  |
| <p style="background-color: #8B4513">　　　</p> | SADDLE_BROWN                                                       | <span style="white-space:nowrap">Saddle Brown</span>          | #8B4513 | 139,69,19   | 25,86,55    |
| <p style="background-color: #FA8072">　　　</p> | SALMON                                                             | <span style="white-space:nowrap">Salmon</span>          | #FA8072 | 250,128,114 | 6,54,98     |
| <p style="background-color: #FF8099">　　　</p> | SALMON_PINK                                                        | <span style="white-space:nowrap">Salmon Pink</span>         | #FF8099 | 255,128,153 | 348,50,100  |
| <p style="background-color: #4D80E6">　　　</p> | SALVIA_BLUE                                                        | <span style="white-space:nowrap">Salvia Blue</span>        | #4D80E6 | 77,128,230  | 220,67,90   |
| <p style="background-color: #E6C3C3">　　　</p> | SAND_BEIGE                                                         | <span style="white-space:nowrap">Sand Beige</span>          | #E6C3C3 | 230,195,195 | 0,15,90     |
| <p style="background-color: #F4A460">　　　</p> | SAND_BROWN                                                         | <span style="white-space:nowrap">Sandy Brown</span>          | #F4A460 | 244,164,96  | 28,61,96    |
| <p style="background-color: #082567">　　　</p> | SAPPHIRE                                                           | <span style="white-space:nowrap">Sapphire</span>    | #082567 | 8,37,103    | 222,92,40   |
| <p style="background-color: #4798B3">　　　</p> | SAXE_BLUE                                                          | <span style="white-space:nowrap">Saxe Blue</span>        | #4798B3 | 71,152,179  | 195,60,70   |
| <p style="background-color: #FF2400">　　　</p> | SCARLET                                                            | <span style="white-space:nowrap">Scarlet</span>     | #FF2400 | 255,36,0    | 8,100,100   |
| <p style="background-color: #FFF5EE">　　　</p> | SEASHELL                                                           | <span style="white-space:nowrap">Seashell</span>          | #FFF5EE | 255,245,238 | 25,7,100    |
| <p style="background-color: #2E8B57">　　　</p> | SEA_GREEN                                                          | <span style="white-space:nowrap">Sea Green</span>          | #2E8B57 | 46,139,87   | 146,67,55   |
| <p style="background-color: #704214">　　　</p> | SEPIA                                                              | <span style="white-space:nowrap">Sepia</span>    | #704214 | 112,66,20   | 30,82,44    |
| <p style="background-color: #FFB3BF">　　　</p> | SHELL_PINK                                                         | <span style="white-space:nowrap">Shell Pink</span>         | #FFB3BF | 255,179,191 | 351,30,100  |
| <p style="background-color: #A0522D">　　　</p> | SIENNA                                                             | <span style="white-space:nowrap">Sienna</span>          | #A0522D | 160,82,45   | 19,72,63    |
| <p style="background-color: #C0C0C0">　　　</p> | SILVER                                                             | <span style="white-space:nowrap">Silver</span>           | #C0C0C0 | 192,192,192 | 0,0,75      |
| <p style="background-color: #87CEEB">　　　</p> | SKY_BLUE                                                           | <span style="white-space:nowrap">Sky Blue</span>         | #87CEEB | 135,206,235 | 197,43,92   |
| <p style="background-color: #6A5ACD">　　　</p> | SLATE_BLUE                                                         | <span style="white-space:nowrap">Slate Blue</span>          | #6A5ACD | 106,90,205  | 248,56,80   |
| <p style="background-color: #708090">　　　</p> | SLATE_GRAY                                                         | <span style="white-space:nowrap">Slate Gray</span>          | #708090 | 112,128,144 | 210,22,56   |
| <p style="background-color: #FFFAFA">　　　</p> | SNOW                                                               | <span style="white-space:nowrap">Snow</span>           | #FFFAFA | 255,250,250 | 0,2,100     |
| <p style="background-color: #FF73B3">　　　</p> | SPINEL_RED                                                         | <span style="white-space:nowrap">Spinel Red</span>        | #FF73B3 | 255,115,179 | 333,55,100  |
| <p style="background-color: #00FF80">　　　</p> | SPRING_GREEN                                                       | <span style="white-space:nowrap">Spring Green</span>          | #00FF80 | 0,255,128   | 150,100,100 |
| <p style="background-color: #4682B4">　　　</p> | STEEL_BLUE                                                         | <span style="white-space:nowrap">Steel Blue</span>          | #4682B4 | 70,130,180  | 207,61,71   |
| <p style="background-color: #006374">　　　</p> | STRONG_BLUE                                                        | <span style="white-space:nowrap">Strong Blue</span>          | #006374 | 0,99,116    | 189,100,45  |
| <p style="background-color: #E60000">　　　</p> | STRONG_RED                                                         | <span style="white-space:nowrap">Strong Red</span>          | #E60000 | 230,0,0     | 0,100,90    |
| <p style="background-color: #FF7300">　　　</p> | SUN_ORANGE                                                         | <span style="white-space:nowrap">Sun Orange</span>          | #FF7300 | 255,115,0   | 27,100,100  |
| <p style="background-color: #D2B48C">　　　</p> | TAN                                                                | <span style="white-space:nowrap">Tan</span>          | #D2B48C | 210,180,140 | 34,33,82    |
| <p style="background-color: #F28500">　　　</p> | TANGERINE                                                          | <span style="white-space:nowrap">Tangerine</span>           | #F28500 | 242,133,0   | 33,100,95   |
| <p style="background-color: #FFCC00">　　　</p> | TANGERINE_YELLOW                                                   | <span style="white-space:nowrap">Tangerine Yellow</span>          | #FFCC00 | 255,204,0   | 48,100,100  |
| <p style="background-color: #008080">　　　</p> | TEAL                                                               | <span style="white-space:nowrap">Teal</span>     | #008080 | 0,128,128   | 180,100,50  |
| <p style="background-color: #D8BFD8">　　　</p> | THISTLE                                                            | <span style="white-space:nowrap">Thistle</span>          | #D8BFD8 | 216,191,216 | 300,12,85   |
| <p style="background-color: #FF6347">　　　</p> | TOMATO                                                             | <span style="white-space:nowrap">Tomato</span>         | #FF6347 | 255,99,71   | 9,72,100    |
| <p style="background-color: #FF8033">　　　</p> | TROPICAL_ORANGE                                                    | <span style="white-space:nowrap">Tropical Orange</span>         | #FF8033 | 255,128,51  | 23,80,100   |
| <p style="background-color: #30D5C8">　　　</p> | TURQUOISE                                                          | <span style="white-space:nowrap">Turquoise</span>    | #30D5C8 | 48,213,200  | 210,100,100 |
| <p style="background-color: #00FFEF">　　　</p> | TURQUOISE_BLUE                                                     | <span style="white-space:nowrap">Turquoise Blue</span>        | #00FFEF | 0,255,239   | 176,100,100 |
| <p style="background-color: #4DE680">　　　</p> | TURQUOISE_GREEN                                                    | <span style="white-space:nowrap">Turquoise Green</span>        | #4DE680 | 77,230,128  | 140,67,90   |
| <p style="background-color: #0033FF">　　　</p> | ULTRAMARINE                                                        | <span style="white-space:nowrap">Ultramarine</span>        | #0033FF | 0,51,255    | 228,100,100 |
| <p style="background-color: #E34234">　　　</p> | VERMILION                                                          | <span style="white-space:nowrap">Vermilion</span>          | #E34234 | 227,66,52   | 5,77,89     |
| <p style="background-color: #73E68C">　　　</p> | VERY_LIGHT_MALACHITE_GREEN                                         | <span style="white-space:nowrap">Malachite</span>        | #73E68C | 115,230,140 | 133,50,90   |
| <p style="background-color: #8000FF">　　　</p> | VIOLET                                                             | <span style="white-space:nowrap">Violet</span>          | #8000FF | 128,0,255   | 270,100,100 |
| <p style="background-color: #127436">　　　</p> | VIRIDIAN                                                           | <span style="white-space:nowrap">Viridian</span>          | #127436 | 18,116,54   | 142,84,45   |
| <p style="background-color: #5686BF">　　　</p> | WEDGWOOD_BLUE                                                      | <span style="white-space:nowrap">Wedgwood Blue</span>      | #5686BF | 86,134,191  | 213,55,75   |
| <p style="background-color: #F5DEB3">　　　</p> | WHEAT                                                              | <span style="white-space:nowrap">Wheat</span>          | #F5DEB3 | 245,222,179 | 39,27,96    |
| <p style="background-color: #FFFFFF">　　　</p> | WHITE                                                              | <span style="white-space:nowrap">White</span>           | #FFFFFF | 255,255,255 | 0,0,100     |
| <p style="background-color: #F5F5F5">　　　</p> | WHITE_SMOKE                                                        | <span style="white-space:nowrap">White Smoke</span>          | #F5F5F5 | 245,245,245 | 0,0,96      |
| <p style="background-color: #C9A0DC">　　　</p> | WISTERIA                                                           | <span style="white-space:nowrap">Wisteria</span>          | #C9A0DC | 201,160,220 | 281,27,86   |
| <p style="background-color: #FFFF00">　　　</p> | YELLOW                                                             | <span style="white-space:nowrap">Yellow</span>           | #FFFF00 | 255,255,0   | 60,100,100  |
| <p style="background-color: #9ACD32">　　　</p> | YELLOW_GREEN                                                       | <span style="white-space:nowrap">Yellow Green</span>          | #9ACD32 | 154,205,50  | 80,76,80    |

## Material Color List

Material Color is the color scheme used in Material Design.

Material Design is a visual language and design system developed by Google, featuring a nearly flat style with vibrant color schemes.

In the Material Color list, variable names containing underscores and numbers represent color shades. Each color uses the 500 shade as the default representative (i.e. `colors.material.RED` is equivalent to `colors.material.RED_500`, except for black and white). Variables containing `A`, such as `RED_A400`, represent accent colors (corresponding to the English term "Accent").

Usage:

```js
colors.material.ORANGE;
```

> See also: [materialui.co](https://materialui.co/colors/)

|                      Color                      | Variable Name                                                                   | Color Name                                              | Hex Code  | RGB         | HSV         |
|:--------------------------------------------:|-----------------------------------------------------------------------|---------------------------------------------------|---------|-------------|-------------|
| <p style="background-color: #FFEBEE">　　　</p> | RED_50                                                                | <span style="white-space:nowrap">Red (50)</span>    | #FFEBEE | 255,235,238 | 351,8,100   |           
| <p style="background-color: #FFCDD2">　　　</p> | RED_100                                                               | <span style="white-space:nowrap">Red (100)</span>   | #FFCDD2 | 255,205,210 | 354,20,100  |
| <p style="background-color: #EF9A9A">　　　</p> | RED_200                                                               | <span style="white-space:nowrap">Red (200)</span>   | #EF9A9A | 239,154,154 | 0,36,94     |
| <p style="background-color: #E57373">　　　</p> | RED_300                                                               | <span style="white-space:nowrap">Red (300)</span>   | #E57373 | 229,115,115 | 0,50,90     |
| <p style="background-color: #EF5350">　　　</p> | RED_400                                                               | <span style="white-space:nowrap">Red (400)</span>   | #EF5350 | 239,83,80   | 1,67,94     |
| <p style="background-color: #F44336">　　　</p> | <span style="white-space:nowrap">RED_500 / RED</span>                 | <span style="white-space:nowrap">Red (500)</span>   | #F44336 | 244,67,54   | 4,78,96     |
| <p style="background-color: #E53935">　　　</p> | RED_600                                                               | <span style="white-space:nowrap">Red (600)</span>   | #E53935 | 229,57,53   | 1,77,90     |
| <p style="background-color: #D32F2F">　　　</p> | RED_700                                                               | <span style="white-space:nowrap">Red (700)</span>   | #D32F2F | 211,47,47   | 0,78,83     |
| <p style="background-color: #C62828">　　　</p> | RED_800                                                               | <span style="white-space:nowrap">Red (800)</span>   | #C62828 | 198,40,40   | 0,80,78     |
| <p style="background-color: #B71C1C">　　　</p> | RED_900                                                               | <span style="white-space:nowrap">Red (900)</span>   | #B71C1C | 183,28,28   | 0,85,72     |
| <p style="background-color: #FF8A80">　　　</p> | RED_A100                                                              | <span style="white-space:nowrap">Red (A100)</span>  | #FF8A80 | 255,138,128 | 5,50,100    |
| <p style="background-color: #FF5252">　　　</p> | RED_A200                                                              | <span style="white-space:nowrap">Red (A200)</span>  | #FF5252 | 255,82,82   | 0,68,100    |
| <p style="background-color: #FF1744">　　　</p> | RED_A400                                                              | <span style="white-space:nowrap">Red (A400)</span>  | #FF1744 | 255,23,68   | 348,91,100  |
| <p style="background-color: #D50000">　　　</p> | RED_A700                                                              | <span style="white-space:nowrap">Red (A700)</span>  | #D50000 | 213,0,0     | 0,100,84    |
| <p style="background-color: #FCE4EC">　　　</p> | PINK_50                                                               | <span style="white-space:nowrap">Pink (50)</span>   | #FCE4EC | 252,228,236 | 340,10,99   |
| <p style="background-color: #F8BBD0">　　　</p> | PINK_100                                                              | <span style="white-space:nowrap">Pink (100)</span>  | #F8BBD0 | 248,187,208 | 339,25,97   |
| <p style="background-color: #F48FB1">　　　</p> | PINK_200                                                              | <span style="white-space:nowrap">Pink (200)</span>  | #F48FB1 | 244,143,177 | 340,41,96   |
| <p style="background-color: #F06292">　　　</p> | PINK_300                                                              | <span style="white-space:nowrap">Pink (300)</span>  | #F06292 | 240,98,146  | 340,59,94   |
| <p style="background-color: #EC407A">　　　</p> | PINK_400                                                              | <span style="white-space:nowrap">Pink (400)</span>  | #EC407A | 236,64,122  | 340,73,93   |
| <p style="background-color: #E91E63">　　　</p> | <span style="white-space:nowrap">PINK_500 / PINK</span>               | <span style="white-space:nowrap">Pink (500)</span>  | #E91E63 | 233,30,99   | 340,87,91   |
| <p style="background-color: #D81B60">　　　</p> | PINK_600                                                              | <span style="white-space:nowrap">Pink (600)</span>  | #D81B60 | 216,27,96   | 338,88,85   |
| <p style="background-color: #C2185B">　　　</p> | PINK_700                                                              | <span style="white-space:nowrap">Pink (700)</span>  | #C2185B | 194,24,91   | 336,88,76   |
| <p style="background-color: #AD1457">　　　</p> | PINK_800                                                              | <span style="white-space:nowrap">Pink (800)</span>  | #AD1457 | 173,20,87   | 334,88,68   |
| <p style="background-color: #880E4F">　　　</p> | PINK_900                                                              | <span style="white-space:nowrap">Pink (900)</span>  | #880E4F | 136,14,79   | 328,90,53   |
| <p style="background-color: #FF80AB">　　　</p> | PINK_A100                                                             | <span style="white-space:nowrap">Pink (A100)</span> | #FF80AB | 255,128,171 | 340,50,100  |
| <p style="background-color: #FF4081">　　　</p> | PINK_A200                                                             | <span style="white-space:nowrap">Pink (A200)</span> | #FF4081 | 255,64,129  | 340,75,100  |
| <p style="background-color: #F50057">　　　</p> | PINK_A400                                                             | <span style="white-space:nowrap">Pink (A400)</span> | #F50057 | 245,0,87    | 339,100,96  |
| <p style="background-color: #C51162">　　　</p> | PINK_A700                                                             | <span style="white-space:nowrap">Pink (A700)</span> | #C51162 | 197,17,98   | 333,91,77   |
| <p style="background-color: #F3E5F5">　　　</p> | PURPLE_50                                                             | <span style="white-space:nowrap">Purple (50)</span>    | #F3E5F5 | 243,229,245 | 293,7,96    |
| <p style="background-color: #E1BEE7">　　　</p> | PURPLE_100                                                            | <span style="white-space:nowrap">Purple (100)</span>   | #E1BEE7 | 225,190,231 | 291,18,91   |
| <p style="background-color: #CE93D8">　　　</p> | PURPLE_200                                                            | <span style="white-space:nowrap">Purple (200)</span>   | #CE93D8 | 206,147,216 | 291,32,85   |
| <p style="background-color: #BA68C8">　　　</p> | PURPLE_300                                                            | <span style="white-space:nowrap">Purple (300)</span>   | #BA68C8 | 186,104,200 | 291,48,78   |
| <p style="background-color: #AB47BC">　　　</p> | PURPLE_400                                                            | <span style="white-space:nowrap">Purple (400)</span>   | #AB47BC | 171,71,188  | 291,62,74   |
| <p style="background-color: #9C27B0">　　　</p> | <span style="white-space:nowrap">PURPLE_500 / PURPLE</span>           | <span style="white-space:nowrap">Purple (500)</span>   | #9C27B0 | 156,39,176  | 291,78,69   |
| <p style="background-color: #8E24AA">　　　</p> | PURPLE_600                                                            | <span style="white-space:nowrap">Purple (600)</span>   | #8E24AA | 142,36,170  | 287,79,67   |
| <p style="background-color: #7B1FA2">　　　</p> | PURPLE_700                                                            | <span style="white-space:nowrap">Purple (700)</span>   | #7B1FA2 | 123,31,162  | 282,81,64   |
| <p style="background-color: #6A1B9A">　　　</p> | PURPLE_800                                                            | <span style="white-space:nowrap">Purple (800)</span>   | #6A1B9A | 106,27,154  | 277,82,60   |
| <p style="background-color: #4A148C">　　　</p> | PURPLE_900                                                            | <span style="white-space:nowrap">Purple (900)</span>   | #4A148C | 74,20,140   | 267,86,55   |
| <p style="background-color: #EA80FC">　　　</p> | PURPLE_A100                                                           | <span style="white-space:nowrap">Purple (A100)</span>  | #EA80FC | 234,128,252 | 291,49,99   |
| <p style="background-color: #E040FB">　　　</p> | PURPLE_A200                                                           | <span style="white-space:nowrap">Purple (A200)</span>  | #E040FB | 224,64,251  | 291,75,98   |
| <p style="background-color: #D500F9">　　　</p> | PURPLE_A400                                                           | <span style="white-space:nowrap">Purple (A400)</span>  | #D500F9 | 213,0,249   | 291,100,98  |
| <p style="background-color: #AA00FF">　　　</p> | PURPLE_A700                                                           | <span style="white-space:nowrap">Purple (A700)</span>  | #AA00FF | 170,0,255   | 280,100,100 |
| <p style="background-color: #EDE7F6">　　　</p> | DEEP_PURPLE_50                                                        | <span style="white-space:nowrap">Deep Purple (50)</span>   | #EDE7F6 | 237,231,246 | 264,6,96    |
| <p style="background-color: #D1C4E9">　　　</p> | DEEP_PURPLE_100                                                       | <span style="white-space:nowrap">Deep Purple (100)</span>  | #D1C4E9 | 209,196,233 | 261,16,91   |
| <p style="background-color: #B39DDB">　　　</p> | DEEP_PURPLE_200                                                       | <span style="white-space:nowrap">Deep Purple (200)</span>  | #B39DDB | 179,157,219 | 261,28,86   |
| <p style="background-color: #9575CD">　　　</p> | DEEP_PURPLE_300                                                       | <span style="white-space:nowrap">Deep Purple (300)</span>  | #9575CD | 149,117,205 | 262,43,80   |
| <p style="background-color: #7E57C2">　　　</p> | DEEP_PURPLE_400                                                       | <span style="white-space:nowrap">Deep Purple (400)</span>  | #7E57C2 | 126,87,194  | 262,55,76   |
| <p style="background-color: #673AB7">　　　</p> | <span style="white-space:nowrap">DEEP_PURPLE_500 / DEEP_PURPLE</span> | <span style="white-space:nowrap">Deep Purple (500)</span>  | #673AB7 | 103,58,183  | 262,68,72   |
| <p style="background-color: #5E35B1">　　　</p> | DEEP_PURPLE_600                                                       | <span style="white-space:nowrap">Deep Purple (600)</span>  | #5E35B1 | 94,53,177   | 260,70,69   |
| <p style="background-color: #512DA8">　　　</p> | DEEP_PURPLE_700                                                       | <span style="white-space:nowrap">Deep Purple (700)</span>  | #512DA8 | 81,45,168   | 258,73,66   |
| <p style="background-color: #4527A0">　　　</p> | DEEP_PURPLE_800                                                       | <span style="white-space:nowrap">Deep Purple (800)</span>  | #4527A0 | 69,39,160   | 255,76,63   |
| <p style="background-color: #311B92">　　　</p> | DEEP_PURPLE_900                                                       | <span style="white-space:nowrap">Deep Purple (900)</span>  | #311B92 | 49,27,146   | 251,82,57   |
| <p style="background-color: #B388FF">　　　</p> | DEEP_PURPLE_A100                                                      | <span style="white-space:nowrap">Deep Purple (A100)</span> | #B388FF | 179,136,255 | 262,47,100  |
| <p style="background-color: #7C4DFF">　　　</p> | DEEP_PURPLE_A200                                                      | <span style="white-space:nowrap">Deep Purple (A200)</span> | #7C4DFF | 124,77,255  | 256,70,100  |
| <p style="background-color: #651FFF">　　　</p> | DEEP_PURPLE_A400                                                      | <span style="white-space:nowrap">Deep Purple (A400)</span> | #651FFF | 101,31,255  | 259,88,100  |
| <p style="background-color: #6200EA">　　　</p> | DEEP_PURPLE_A700                                                      | <span style="white-space:nowrap">Deep Purple (A700)</span> | #6200EA | 98,0,234    | 265,100,92  |
| <p style="background-color: #E8EAF6">　　　</p> | INDIGO_50                                                             | <span style="white-space:nowrap">Indigo (50)</span>   | #E8EAF6 | 232,234,246 | 231,6,96    |
| <p style="background-color: #C5CAE9">　　　</p> | INDIGO_100                                                            | <span style="white-space:nowrap">Indigo (100)</span>  | #C5CAE9 | 197,202,233 | 232,15,91   |
| <p style="background-color: #9FA8DA">　　　</p> | INDIGO_200                                                            | <span style="white-space:nowrap">Indigo (200)</span>  | #9FA8DA | 159,168,218 | 231,27,85   |
| <p style="background-color: #7986CB">　　　</p> | INDIGO_300                                                            | <span style="white-space:nowrap">Indigo (300)</span>  | #7986CB | 121,134,203 | 230,40,80   |
| <p style="background-color: #5C6BC0">　　　</p> | INDIGO_400                                                            | <span style="white-space:nowrap">Indigo (400)</span>  | #5C6BC0 | 92,107,192  | 231,52,75   |
| <p style="background-color: #3F51B5">　　　</p> | <span style="white-space:nowrap">INDIGO_500 / INDIGO</span>           | <span style="white-space:nowrap">Indigo (500)</span>  | #3F51B5 | 63,81,181   | 231,65,71   |
| <p style="background-color: #3949AB">　　　</p> | INDIGO_600                                                            | <span style="white-space:nowrap">Indigo (600)</span>  | #3949AB | 57,73,171   | 232,67,67   |
| <p style="background-color: #303F9F">　　　</p> | INDIGO_700                                                            | <span style="white-space:nowrap">Indigo (700)</span>  | #303F9F | 48,63,159   | 232,70,62   |
| <p style="background-color: #283593">　　　</p> | INDIGO_800                                                            | <span style="white-space:nowrap">Indigo (800)</span>  | #283593 | 40,53,147   | 233,73,58   |
| <p style="background-color: #1A237E">　　　</p> | INDIGO_900                                                            | <span style="white-space:nowrap">Indigo (900)</span>  | #1A237E | 26,35,126   | 235,79,49   |
| <p style="background-color: #8C9EFF">　　　</p> | INDIGO_A100                                                           | <span style="white-space:nowrap">Indigo (A100)</span> | #8C9EFF | 140,158,255 | 231,45,100  |
| <p style="background-color: #536DFE">　　　</p> | INDIGO_A200                                                           | <span style="white-space:nowrap">Indigo (A200)</span> | #536DFE | 83,109,254  | 231,67,100  |
| <p style="background-color: #3D5AFE">　　　</p> | INDIGO_A400                                                           | <span style="white-space:nowrap">Indigo (A400)</span> | #3D5AFE | 61,90,254   | 231,76,100  |
| <p style="background-color: #304FFE">　　　</p> | INDIGO_A700                                                           | <span style="white-space:nowrap">Indigo (A700)</span> | #304FFE | 48,79,254   | 231,81,100  |
| <p style="background-color: #E3F2FD">　　　</p> | BLUE_50                                                               | <span style="white-space:nowrap">Blue (50)</span>    | #E3F2FD | 227,242,253 | 205,10,99   |
| <p style="background-color: #BBDEFB">　　　</p> | BLUE_100                                                              | <span style="white-space:nowrap">Blue (100)</span>   | #BBDEFB | 187,222,251 | 207,25,98   |
| <p style="background-color: #90CAF9">　　　</p> | BLUE_200                                                              | <span style="white-space:nowrap">Blue (200)</span>   | #90CAF9 | 144,202,249 | 207,42,98   |
| <p style="background-color: #64B5F6">　　　</p> | BLUE_300                                                              | <span style="white-space:nowrap">Blue (300)</span>   | #64B5F6 | 100,181,246 | 207,59,96   |
| <p style="background-color: #42A5F5">　　　</p> | BLUE_400                                                              | <span style="white-space:nowrap">Blue (400)</span>   | #42A5F5 | 66,165,245  | 207,73,96   |
| <p style="background-color: #2196F3">　　　</p> | <span style="white-space:nowrap">BLUE_500 / BLUE</span>               | <span style="white-space:nowrap">Blue (500)</span>   | #2196F3 | 33,150,243  | 207,86,95   |
| <p style="background-color: #1E88E5">　　　</p> | BLUE_600                                                              | <span style="white-space:nowrap">Blue (600)</span>   | #1E88E5 | 30,136,229  | 208,87,90   |
| <p style="background-color: #1976D2">　　　</p> | BLUE_700                                                              | <span style="white-space:nowrap">Blue (700)</span>   | #1976D2 | 25,118,210  | 210,88,82   |
| <p style="background-color: #1565C0">　　　</p> | BLUE_800                                                              | <span style="white-space:nowrap">Blue (800)</span>   | #1565C0 | 21,101,192  | 212,89,75   |
| <p style="background-color: #0D47A1">　　　</p> | BLUE_900                                                              | <span style="white-space:nowrap">Blue (900)</span>   | #0D47A1 | 13,71,161   | 216,92,63   |
| <p style="background-color: #82B1FF">　　　</p> | BLUE_A100                                                             | <span style="white-space:nowrap">Blue (A100)</span>  | #82B1FF | 130,177,255 | 217,49,100  |
| <p style="background-color: #448AFF">　　　</p> | BLUE_A200                                                             | <span style="white-space:nowrap">Blue (A200)</span>  | #448AFF | 68,138,255  | 218,73,100  |
| <p style="background-color: #2979FF">　　　</p> | BLUE_A400                                                             | <span style="white-space:nowrap">Blue (A400)</span>  | #2979FF | 41,121,255  | 218,84,100  |
| <p style="background-color: #2962FF">　　　</p> | BLUE_A700                                                             | <span style="white-space:nowrap">Blue (A700)</span>  | #2962FF | 41,98,255   | 224,84,100  |
| <p style="background-color: #E1F5FE">　　　</p> | LIGHT_BLUE_50                                                         | <span style="white-space:nowrap">Light Blue (50)</span>   | #E1F5FE | 225,245,254 | 199,11,100  |
| <p style="background-color: #B3E5FC">　　　</p> | LIGHT_BLUE_100                                                        | <span style="white-space:nowrap">Light Blue (100)</span>  | #B3E5FC | 179,229,252 | 199,29,99   |
| <p style="background-color: #81D4FA">　　　</p> | LIGHT_BLUE_200                                                        | <span style="white-space:nowrap">Light Blue (200)</span>  | #81D4FA | 129,212,250 | 199,48,98   |
| <p style="background-color: #4FC3F7">　　　</p> | LIGHT_BLUE_300                                                        | <span style="white-space:nowrap">Light Blue (300)</span>  | #4FC3F7 | 79,195,247  | 199,68,97   |
| <p style="background-color: #29B6FC">　　　</p> | LIGHT_BLUE_400                                                        | <span style="white-space:nowrap">Light Blue (400)</span>  | #29B6FC | 41,182,252  | 200,84,99   |
| <p style="background-color: #03A9F4">　　　</p> | <span style="white-space:nowrap">LIGHT_BLUE_500 / LIGHT_BLUE</span>   | <span style="white-space:nowrap">Light Blue (500)</span>  | #03A9F4 | 3,169,244   | 199,99,96   |
| <p style="background-color: #039BE5">　　　</p> | LIGHT_BLUE_600                                                        | <span style="white-space:nowrap">Light Blue (600)</span>  | #039BE5 | 3,155,229   | 200,99,90   |
| <p style="background-color: #0288D1">　　　</p> | LIGHT_BLUE_700                                                        | <span style="white-space:nowrap">Light Blue (700)</span>  | #0288D1 | 2,136,209   | 201,99,82   |
| <p style="background-color: #0277BD">　　　</p> | LIGHT_BLUE_800                                                        | <span style="white-space:nowrap">Light Blue (800)</span>  | #0277BD | 2,119,189   | 202,99,74   |
| <p style="background-color: #01579B">　　　</p> | LIGHT_BLUE_900                                                        | <span style="white-space:nowrap">Light Blue (900)</span>  | #01579B | 1,87,155    | 206,99,61   |
| <p style="background-color: #80D8FF">　　　</p> | LIGHT_BLUE_A100                                                       | <span style="white-space:nowrap">Light Blue (A100)</span> | #80D8FF | 128,216,255 | 198,50,100  |
| <p style="background-color: #40C4FF">　　　</p> | LIGHT_BLUE_A200                                                       | <span style="white-space:nowrap">Light Blue (A200)</span> | #40C4FF | 64,196,255  | 199,75,100  |
| <p style="background-color: #00B0FF">　　　</p> | LIGHT_BLUE_A400                                                       | <span style="white-space:nowrap">Light Blue (A400)</span> | #00B0FF | 0,176,255   | 199,100,100 |
| <p style="background-color: #0091EA">　　　</p> | LIGHT_BLUE_A700                                                       | <span style="white-space:nowrap">Light Blue (A700)</span> | #0091EA | 0,145,234   | 203,100,92  |
| <p style="background-color: #E0F7FA">　　　</p> | CYAN_50                                                               | <span style="white-space:nowrap">Cyan (50)</span>    | #E0F7FA | 224,247,250 | 187,10,98   |
| <p style="background-color: #B2EBF2">　　　</p> | CYAN_100                                                              | <span style="white-space:nowrap">Cyan (100)</span>   | #B2EBF2 | 178,235,242 | 187,26,95   |
| <p style="background-color: #80DEEA">　　　</p> | CYAN_200                                                              | <span style="white-space:nowrap">Cyan (200)</span>   | #80DEEA | 128,222,234 | 187,45,92   |
| <p style="background-color: #4DD0E1">　　　</p> | CYAN_300                                                              | <span style="white-space:nowrap">Cyan (300)</span>   | #4DD0E1 | 77,208,225  | 187,66,88   |
| <p style="background-color: #26C6DA">　　　</p> | CYAN_400                                                              | <span style="white-space:nowrap">Cyan (400)</span>   | #26C6DA | 38,198,218  | 187,83,85   |
| <p style="background-color: #00BCD4">　　　</p> | <span style="white-space:nowrap">CYAN_500 / CYAN</span>               | <span style="white-space:nowrap">Cyan (500)</span>   | #00BCD4 | 0,188,212   | 187,100,83  |
| <p style="background-color: #00ACC1">　　　</p> | CYAN_600                                                              | <span style="white-space:nowrap">Cyan (600)</span>   | #00ACC1 | 0,172,193   | 187,100,76  |
| <p style="background-color: #0097A7">　　　</p> | CYAN_700                                                              | <span style="white-space:nowrap">Cyan (700)</span>   | #0097A7 | 0,151,167   | 186,100,65  |
| <p style="background-color: #00838F">　　　</p> | CYAN_800                                                              | <span style="white-space:nowrap">Cyan (800)</span>   | #00838F | 0,131,143   | 185,100,56  |
| <p style="background-color: #006064">　　　</p> | CYAN_900                                                              | <span style="white-space:nowrap">Cyan (900)</span>   | #006064 | 0,96,100    | 182,100,39  |
| <p style="background-color: #84FFFF">　　　</p> | CYAN_A100                                                             | <span style="white-space:nowrap">Cyan (A100)</span>  | #84FFFF | 132,255,255 | 180,48,100  |
| <p style="background-color: #18FFFF">　　　</p> | CYAN_A200                                                             | <span style="white-space:nowrap">Cyan (A200)</span>  | #18FFFF | 24,255,255  | 180,91,100  |
| <p style="background-color: #00E5FF">　　　</p> | CYAN_A400                                                             | <span style="white-space:nowrap">Cyan (A400)</span>  | #00E5FF | 0,229,255   | 186,100,100 |
| <p style="background-color: #00B8D4">　　　</p> | CYAN_A700                                                             | <span style="white-space:nowrap">Cyan (A700)</span>  | #00B8D4 | 0,184,212   | 188,100,83  |
| <p style="background-color: #E0F2F1">　　　</p> | TEAL_50                                                               | <span style="white-space:nowrap">Teal (50)</span>   | #E0F2F1 | 224,242,241 | 177,7,95    |
| <p style="background-color: #B2DFDB">　　　</p> | TEAL_100                                                              | <span style="white-space:nowrap">Teal (100)</span>  | #B2DFDB | 178,223,219 | 175,20,87   |
| <p style="background-color: #80CBC4">　　　</p> | TEAL_200                                                              | <span style="white-space:nowrap">Teal (200)</span>  | #80CBC4 | 128,203,196 | 174,37,80   |
| <p style="background-color: #4DB6AC">　　　</p> | TEAL_300                                                              | <span style="white-space:nowrap">Teal (300)</span>  | #4DB6AC | 77,182,172  | 174,58,71   |
| <p style="background-color: #26A69A">　　　</p> | TEAL_400                                                              | <span style="white-space:nowrap">Teal (400)</span>  | #26A69A | 38,166,154  | 174,77,65   |
| <p style="background-color: #009688">　　　</p> | <span style="white-space:nowrap">TEAL_500 / TEAL</span>               | <span style="white-space:nowrap">Teal (500)</span>  | #009688 | 0,150,136   | 174,100,59  |
| <p style="background-color: #00897B">　　　</p> | TEAL_600                                                              | <span style="white-space:nowrap">Teal (600)</span>  | #00897B | 0,137,123   | 174,100,54  |
| <p style="background-color: #00796B">　　　</p> | TEAL_700                                                              | <span style="white-space:nowrap">Teal (700)</span>  | #00796B | 0,121,107   | 173,100,47  |
| <p style="background-color: #00695C">　　　</p> | TEAL_800                                                              | <span style="white-space:nowrap">Teal (800)</span>  | #00695C | 0,105,92    | 173,100,41  |
| <p style="background-color: #004D40">　　　</p> | TEAL_900                                                              | <span style="white-space:nowrap">Teal (900)</span>  | #004D40 | 0,77,64     | 170,100,30  |
| <p style="background-color: #A7FFEB">　　　</p> | TEAL_A100                                                             | <span style="white-space:nowrap">Teal (A100)</span> | #A7FFEB | 167,255,235 | 166,35,100  |
| <p style="background-color: #64FFDA">　　　</p> | TEAL_A200                                                             | <span style="white-space:nowrap">Teal (A200)</span> | #64FFDA | 100,255,218 | 166,61,100  |
| <p style="background-color: #1DE9B6">　　　</p> | TEAL_A400                                                             | <span style="white-space:nowrap">Teal (A400)</span> | #1DE9B6 | 29,233,182  | 165,88,91   |
| <p style="background-color: #00BFA5">　　　</p> | TEAL_A700                                                             | <span style="white-space:nowrap">Teal (A700)</span> | #00BFA5 | 0,191,165   | 172,100,75  |
| <p style="background-color: #E8F5E9">　　　</p> | GREEN_50                                                              | <span style="white-space:nowrap">Green (50)</span>    | #E8F5E9 | 232,245,233 | 125,5,96    |
| <p style="background-color: #C8E6C9">　　　</p> | GREEN_100                                                             | <span style="white-space:nowrap">Green (100)</span>   | #C8E6C9 | 200,230,201 | 122,13,90   |
| <p style="background-color: #A5D6A7">　　　</p> | GREEN_200                                                             | <span style="white-space:nowrap">Green (200)</span>   | #A5D6A7 | 165,214,167 | 122,23,84   |
| <p style="background-color: #81C784">　　　</p> | GREEN_300                                                             | <span style="white-space:nowrap">Green (300)</span>   | #81C784 | 129,199,132 | 123,35,78   |
| <p style="background-color: #66BB6A">　　　</p> | GREEN_400                                                             | <span style="white-space:nowrap">Green (400)</span>   | #66BB6A | 102,187,106 | 123,45,73   |
| <p style="background-color: #4CAF50">　　　</p> | <span style="white-space:nowrap">GREEN_500 / GREEN</span>             | <span style="white-space:nowrap">Green (500)</span>   | #4CAF50 | 76,175,80   | 122,57,69   |
| <p style="background-color: #43A047">　　　</p> | GREEN_600                                                             | <span style="white-space:nowrap">Green (600)</span>   | #43A047 | 67,160,71   | 123,58,63   |
| <p style="background-color: #388E3C">　　　</p> | GREEN_700                                                             | <span style="white-space:nowrap">Green (700)</span>   | #388E3C | 56,142,60   | 123,61,56   |
| <p style="background-color: #2E7D32">　　　</p> | GREEN_800                                                             | <span style="white-space:nowrap">Green (800)</span>   | #2E7D32 | 46,125,50   | 123,63,49   |
| <p style="background-color: #1B5E20">　　　</p> | GREEN_900                                                             | <span style="white-space:nowrap">Green (900)</span>   | #1B5E20 | 27,94,32    | 124,71,37   |
| <p style="background-color: #B9F6CA">　　　</p> | GREEN_A100                                                            | <span style="white-space:nowrap">Green (A100)</span>  | #B9F6CA | 185,246,202 | 137,25,96   |
| <p style="background-color: #69F0AE">　　　</p> | GREEN_A200                                                            | <span style="white-space:nowrap">Green (A200)</span>  | #69F0AE | 105,240,174 | 151,56,94   |
| <p style="background-color: #00E676">　　　</p> | GREEN_A400                                                            | <span style="white-space:nowrap">Green (A400)</span>  | #00E676 | 0,230,118   | 151,100,90  |
| <p style="background-color: #00C853">　　　</p> | GREEN_A700                                                            | <span style="white-space:nowrap">Green (A700)</span>  | #00C853 | 0,200,83    | 145,100,78  |
| <p style="background-color: #F1F8E9">　　　</p> | LIGHT_GREEN_50                                                        | <span style="white-space:nowrap">Light Green (50)</span>   | #F1F8E9 | 241,248,233 | 88,6,97     |
| <p style="background-color: #DCEDC8">　　　</p> | LIGHT_GREEN_100                                                       | <span style="white-space:nowrap">Light Green (100)</span>  | #DCEDC8 | 220,237,200 | 88,16,93    |
| <p style="background-color: #C5E1A5">　　　</p> | LIGHT_GREEN_200                                                       | <span style="white-space:nowrap">Light Green (200)</span>  | #C5E1A5 | 197,225,165 | 88,27,88    |
| <p style="background-color: #AED581">　　　</p> | LIGHT_GREEN_300                                                       | <span style="white-space:nowrap">Light Green (300)</span>  | #AED581 | 174,213,129 | 88,39,84    |
| <p style="background-color: #9CCC65">　　　</p> | LIGHT_GREEN_400                                                       | <span style="white-space:nowrap">Light Green (400)</span>  | #9CCC65 | 156,204,101 | 88,50,80    |
| <p style="background-color: #8BC34A">　　　</p> | <span style="white-space:nowrap">LIGHT_GREEN_500 / LIGHT_GREEN</span> | <span style="white-space:nowrap">Light Green (500)</span>  | #8BC34A | 139,195,74  | 88,62,76    |
| <p style="background-color: #7CB342">　　　</p> | LIGHT_GREEN_600                                                       | <span style="white-space:nowrap">Light Green (600)</span>  | #7CB342 | 124,179,66  | 89,63,70    |
| <p style="background-color: #689F38">　　　</p> | LIGHT_GREEN_700                                                       | <span style="white-space:nowrap">Light Green (700)</span>  | #689F38 | 104,159,56  | 92,65,62    |
| <p style="background-color: #558B2F">　　　</p> | LIGHT_GREEN_800                                                       | <span style="white-space:nowrap">Light Green (800)</span>  | #558B2F | 85,139,47   | 95,66,55    |
| <p style="background-color: #33691E">　　　</p> | LIGHT_GREEN_900                                                       | <span style="white-space:nowrap">Light Green (900)</span>  | #33691E | 51,105,30   | 103,71,41   |
| <p style="background-color: #CCFF90">　　　</p> | LIGHT_GREEN_A100                                                      | <span style="white-space:nowrap">Light Green (A100)</span> | #CCFF90 | 204,255,144 | 88,44,100   |
| <p style="background-color: #B2FF59">　　　</p> | LIGHT_GREEN_A200                                                      | <span style="white-space:nowrap">Light Green (A200)</span> | #B2FF59 | 178,255,89  | 88,65,100   |
| <p style="background-color: #76FF03">　　　</p> | LIGHT_GREEN_A400                                                      | <span style="white-space:nowrap">Light Green (A400)</span> | #76FF03 | 118,255,3   | 93,99,100   |
| <p style="background-color: #64DD17">　　　</p> | LIGHT_GREEN_A700                                                      | <span style="white-space:nowrap">Light Green (A700)</span> | #64DD17 | 100,221,23  | 97,90,87    |
| <p style="background-color: #F9FBE7">　　　</p> | LIME_50                                                               | <span style="white-space:nowrap">Lime (50)</span>   | #F9FBE7 | 249,251,231 | 66,8,98     |
| <p style="background-color: #F0F4C3">　　　</p> | LIME_100                                                              | <span style="white-space:nowrap">Lime (100)</span>  | #F0F4C3 | 240,244,195 | 65,20,96    |
| <p style="background-color: #E6EE9C">　　　</p> | LIME_200                                                              | <span style="white-space:nowrap">Lime (200)</span>  | #E6EE9C | 230,238,156 | 66,34,93    |
| <p style="background-color: #DCE775">　　　</p> | LIME_300                                                              | <span style="white-space:nowrap">Lime (300)</span>  | #DCE775 | 220,231,117 | 66,49,91    |
| <p style="background-color: #D4E157">　　　</p> | LIME_400                                                              | <span style="white-space:nowrap">Lime (400)</span>  | #D4E157 | 212,225,87  | 66,61,88    |
| <p style="background-color: #CDDC39">　　　</p> | <span style="white-space:nowrap">LIME_500 / LIME</span>               | <span style="white-space:nowrap">Lime (500)</span>  | #CDDC39 | 205,220,57  | 66,74,86    |
| <p style="background-color: #C0CA33">　　　</p> | LIME_600                                                              | <span style="white-space:nowrap">Lime (600)</span>  | #C0CA33 | 192,202,51  | 64,75,79    |
| <p style="background-color: #A4B42B">　　　</p> | LIME_700                                                              | <span style="white-space:nowrap">Lime (700)</span>  | #A4B42B | 164,180,43  | 67,76,71    |
| <p style="background-color: #9E9D24">　　　</p> | LIME_800                                                              | <span style="white-space:nowrap">Lime (800)</span>  | #9E9D24 | 158,157,36  | 60,77,62    |
| <p style="background-color: #827717">　　　</p> | LIME_900                                                              | <span style="white-space:nowrap">Lime (900)</span>  | #827717 | 130,119,23  | 54,82,51    |
| <p style="background-color: #F4FF81">　　　</p> | LIME_A100                                                             | <span style="white-space:nowrap">Lime (A100)</span> | #F4FF81 | 244,255,129 | 65,49,100   |
| <p style="background-color: #EEFF41">　　　</p> | LIME_A200                                                             | <span style="white-space:nowrap">Lime (A200)</span> | #EEFF41 | 238,255,65  | 65,75,100   |
| <p style="background-color: #C6FF00">　　　</p> | LIME_A400                                                             | <span style="white-space:nowrap">Lime (A400)</span> | #C6FF00 | 198,255,0   | 73,100,100  |
| <p style="background-color: #AEEA00">　　　</p> | LIME_A700                                                             | <span style="white-space:nowrap">Lime (A700)</span> | #AEEA00 | 174,234,0   | 75,100,92   |
| <p style="background-color: #FFFDE7">　　　</p> | YELLOW_50                                                             | <span style="white-space:nowrap">Yellow (50)</span>    | #FFFDE7 | 255,253,231 | 55,9,100    |
| <p style="background-color: #FFF9C4">　　　</p> | YELLOW_100                                                            | <span style="white-space:nowrap">Yellow (100)</span>   | #FFF9C4 | 255,249,196 | 54,23,100   |
| <p style="background-color: #FFF590">　　　</p> | YELLOW_200                                                            | <span style="white-space:nowrap">Yellow (200)</span>   | #FFF590 | 255,245,144 | 55,44,100   |
| <p style="background-color: #FFF176">　　　</p> | YELLOW_300                                                            | <span style="white-space:nowrap">Yellow (300)</span>   | #FFF176 | 255,241,118 | 54,54,100   |
| <p style="background-color: #FFEE58">　　　</p> | YELLOW_400                                                            | <span style="white-space:nowrap">Yellow (400)</span>   | #FFEE58 | 255,238,88  | 54,65,100   |
| <p style="background-color: #FFEB3B">　　　</p> | <span style="white-space:nowrap">YELLOW_500 / YELLOW</span>           | <span style="white-space:nowrap">Yellow (500)</span>   | #FFEB3B | 255,235,59  | 54,77,100   |
| <p style="background-color: #FDD835">　　　</p> | YELLOW_600                                                            | <span style="white-space:nowrap">Yellow (600)</span>   | #FDD835 | 253,216,53  | 49,79,99    |
| <p style="background-color: #FBC02D">　　　</p> | YELLOW_700                                                            | <span style="white-space:nowrap">Yellow (700)</span>   | #FBC02D | 251,192,45  | 43,82,98    |
| <p style="background-color: #F9A825">　　　</p> | YELLOW_800                                                            | <span style="white-space:nowrap">Yellow (800)</span>   | #F9A825 | 249,168,37  | 37,85,98    |
| <p style="background-color: #F57F17">　　　</p> | YELLOW_900                                                            | <span style="white-space:nowrap">Yellow (900)</span>   | #F57F17 | 245,127,23  | 28,91,96    |
| <p style="background-color: #FFFF82">　　　</p> | YELLOW_A100                                                           | <span style="white-space:nowrap">Yellow (A100)</span>  | #FFFF82 | 255,255,130 | 60,49,100   |
| <p style="background-color: #FFFF00">　　　</p> | YELLOW_A200                                                           | <span style="white-space:nowrap">Yellow (A200)</span>  | #FFFF00 | 255,255,0   | 60,100,100  |
| <p style="background-color: #FFEA00">　　　</p> | YELLOW_A400                                                           | <span style="white-space:nowrap">Yellow (A400)</span>  | #FFEA00 | 255,234,0   | 55,100,100  |
| <p style="background-color: #FFD600">　　　</p> | YELLOW_A700                                                           | <span style="white-space:nowrap">Yellow (A700)</span>  | #FFD600 | 255,214,0   | 50,100,100  |
| <p style="background-color: #FFF8E1">　　　</p> | AMBER_50                                                              | <span style="white-space:nowrap">Amber (50)</span>   | #FFF8E1 | 255,248,225 | 46,12,100   |
| <p style="background-color: #FFECB3">　　　</p> | AMBER_100                                                             | <span style="white-space:nowrap">Amber (100)</span>  | #FFECB3 | 255,236,179 | 45,30,100   |
| <p style="background-color: #FFE082">　　　</p> | AMBER_200                                                             | <span style="white-space:nowrap">Amber (200)</span>  | #FFE082 | 255,224,130 | 45,49,100   |
| <p style="background-color: #FFD54F">　　　</p> | AMBER_300                                                             | <span style="white-space:nowrap">Amber (300)</span>  | #FFD54F | 255,213,79  | 46,69,100   |
| <p style="background-color: #FFCA28">　　　</p> | AMBER_400                                                             | <span style="white-space:nowrap">Amber (400)</span>  | #FFCA28 | 255,202,40  | 45,84,100   |
| <p style="background-color: #FFC107">　　　</p> | <span style="white-space:nowrap">AMBER_500 / AMBER</span>             | <span style="white-space:nowrap">Amber (500)</span>  | #FFC107 | 255,193,7   | 45,97,100   |
| <p style="background-color: #FFB300">　　　</p> | AMBER_600                                                             | <span style="white-space:nowrap">Amber (600)</span>  | #FFB300 | 255,179,0   | 42,100,100  |
| <p style="background-color: #FFA000">　　　</p> | AMBER_700                                                             | <span style="white-space:nowrap">Amber (700)</span>  | #FFA000 | 255,160,0   | 38,100,100  |
| <p style="background-color: #FF8F00">　　　</p> | AMBER_800                                                             | <span style="white-space:nowrap">Amber (800)</span>  | #FF8F00 | 255,143,0   | 34,100,100  |
| <p style="background-color: #FF6F00">　　　</p> | AMBER_900                                                             | <span style="white-space:nowrap">Amber (900)</span>  | #FF6F00 | 255,111,0   | 26,100,100  |
| <p style="background-color: #FFE57F">　　　</p> | AMBER_A100                                                            | <span style="white-space:nowrap">Amber (A100)</span> | #FFE57F | 255,229,127 | 48,50,100   |
| <p style="background-color: #FFD740">　　　</p> | AMBER_A200                                                            | <span style="white-space:nowrap">Amber (A200)</span> | #FFD740 | 255,215,64  | 47,75,100   |
| <p style="background-color: #FFC400">　　　</p> | AMBER_A400                                                            | <span style="white-space:nowrap">Amber (A400)</span> | #FFC400 | 255,196,0   | 46,100,100  |
| <p style="background-color: #FFAB00">　　　</p> | AMBER_A700                                                            | <span style="white-space:nowrap">Amber (A700)</span> | #FFAB00 | 255,171,0   | 40,100,100  |
| <p style="background-color: #FFF3E0">　　　</p> | ORANGE_50                                                             | <span style="white-space:nowrap">Orange (50)</span>    | #FFF3E0 | 255,243,224 | 37,12,100   |
| <p style="background-color: #FFE0B2">　　　</p> | ORANGE_100                                                            | <span style="white-space:nowrap">Orange (100)</span>   | #FFE0B2 | 255,224,178 | 36,30,100   |
| <p style="background-color: #FFCC80">　　　</p> | ORANGE_200                                                            | <span style="white-space:nowrap">Orange (200)</span>   | #FFCC80 | 255,204,128 | 36,50,100   |
| <p style="background-color: #FFB74D">　　　</p> | ORANGE_300                                                            | <span style="white-space:nowrap">Orange (300)</span>   | #FFB74D | 255,183,77  | 36,70,100   |
| <p style="background-color: #FFA726">　　　</p> | ORANGE_400                                                            | <span style="white-space:nowrap">Orange (400)</span>   | #FFA726 | 255,167,38  | 36,85,100   |
| <p style="background-color: #FF9800">　　　</p> | <span style="white-space:nowrap">ORANGE_500 / ORANGE</span>           | <span style="white-space:nowrap">Orange (500)</span>   | #FF9800 | 255,152,0   | 36,100,100  |
| <p style="background-color: #FB8C00">　　　</p> | ORANGE_600                                                            | <span style="white-space:nowrap">Orange (600)</span>   | #FB8C00 | 251,140,0   | 33,100,98   |
| <p style="background-color: #F57C00">　　　</p> | ORANGE_700                                                            | <span style="white-space:nowrap">Orange (700)</span>   | #F57C00 | 245,124,0   | 30,100,96   |
| <p style="background-color: #EF6C00">　　　</p> | ORANGE_800                                                            | <span style="white-space:nowrap">Orange (800)</span>   | #EF6C00 | 239,108,0   | 27,100,94   |
| <p style="background-color: #E65100">　　　</p> | ORANGE_900                                                            | <span style="white-space:nowrap">Orange (900)</span>   | #E65100 | 230,81,0    | 21,100,90   |
| <p style="background-color: #FFD180">　　　</p> | ORANGE_A100                                                           | <span style="white-space:nowrap">Orange (A100)</span>  | #FFD180 | 255,209,128 | 38,50,100   |
| <p style="background-color: #FFAB40">　　　</p> | ORANGE_A200                                                           | <span style="white-space:nowrap">Orange (A200)</span>  | #FFAB40 | 255,171,64  | 34,75,100   |
| <p style="background-color: #FF9100">　　　</p> | ORANGE_A400                                                           | <span style="white-space:nowrap">Orange (A400)</span>  | #FF9100 | 255,145,0   | 34,100,100  |
| <p style="background-color: #FF6D00">　　　</p> | ORANGE_A700                                                           | <span style="white-space:nowrap">Orange (A700)</span>  | #FF6D00 | 255,109,0   | 26,100,100  |
| <p style="background-color: #FBE9A7">　　　</p> | DEEP_ORANGE_50                                                        | <span style="white-space:nowrap">Deep Orange (50)</span>   | #FBE9A7 | 251,233,167 | 47,33,98    |
| <p style="background-color: #FFCCBC">　　　</p> | DEEP_ORANGE_100                                                       | <span style="white-space:nowrap">Deep Orange (100)</span>  | #FFCCBC | 255,204,188 | 14,26,100   |
| <p style="background-color: #FFAB91">　　　</p> | DEEP_ORANGE_200                                                       | <span style="white-space:nowrap">Deep Orange (200)</span>  | #FFAB91 | 255,171,145 | 14,43,100   |
| <p style="background-color: #FF8A65">　　　</p> | DEEP_ORANGE_300                                                       | <span style="white-space:nowrap">Deep Orange (300)</span>  | #FF8A65 | 255,138,101 | 14,60,100   |
| <p style="background-color: #FF7043">　　　</p> | DEEP_ORANGE_400                                                       | <span style="white-space:nowrap">Deep Orange (400)</span>  | #FF7043 | 255,112,67  | 14,74,100   |
| <p style="background-color: #FF5722">　　　</p> | <span style="white-space:nowrap">DEEP_ORANGE_500 / DEEP_ORANGE</span> | <span style="white-space:nowrap">Deep Orange (500)</span>  | #FF5722 | 255,87,34   | 14,87,100   |
| <p style="background-color: #F4511E">　　　</p> | DEEP_ORANGE_600                                                       | <span style="white-space:nowrap">Deep Orange (600)</span>  | #F4511E | 244,81,30   | 14,88,96    |
| <p style="background-color: #E64A19">　　　</p> | DEEP_ORANGE_700                                                       | <span style="white-space:nowrap">Deep Orange (700)</span>  | #E64A19 | 230,74,25   | 14,89,90    |
| <p style="background-color: #D84315">　　　</p> | DEEP_ORANGE_800                                                       | <span style="white-space:nowrap">Deep Orange (800)</span>  | #D84315 | 216,67,21   | 14,90,85    |
| <p style="background-color: #BF360C">　　　</p> | DEEP_ORANGE_900                                                       | <span style="white-space:nowrap">Deep Orange (900)</span>  | #BF360C | 191,54,12   | 14,94,75    |
| <p style="background-color: #FF9E80">　　　</p> | DEEP_ORANGE_A100                                                      | <span style="white-space:nowrap">Deep Orange (A100)</span> | #FF9E80 | 255,158,128 | 14,50,100   |
| <p style="background-color: #FF6E40">　　　</p> | DEEP_ORANGE_A200                                                      | <span style="white-space:nowrap">Deep Orange (A200)</span> | #FF6E40 | 255,110,64  | 14,75,100   |
| <p style="background-color: #FF3D00">　　　</p> | DEEP_ORANGE_A400                                                      | <span style="white-space:nowrap">Deep Orange (A400)</span> | #FF3D00 | 255,61,0    | 14,100,100  |
| <p style="background-color: #DD2600">　　　</p> | DEEP_ORANGE_A700                                                      | <span style="white-space:nowrap">Deep Orange (A700)</span> | #DD2600 | 221,38,0    | 10,100,87   |
| <p style="background-color: #EFEBE9">　　　</p> | BROWN_50                                                              | <span style="white-space:nowrap">Brown (50)</span>    | #EFEBE9 | 239,235,233 | 20,3,94     |
| <p style="background-color: #D7CCC8">　　　</p> | BROWN_100                                                             | <span style="white-space:nowrap">Brown (100)</span>   | #D7CCC8 | 215,204,200 | 16,7,84     |
| <p style="background-color: #BCAAA4">　　　</p> | BROWN_200                                                             | <span style="white-space:nowrap">Brown (200)</span>   | #BCAAA4 | 188,170,164 | 15,13,74    |
| <p style="background-color: #A1887F">　　　</p> | BROWN_300                                                             | <span style="white-space:nowrap">Brown (300)</span>   | #A1887F | 161,136,127 | 16,21,63    |
| <p style="background-color: #8D6E63">　　　</p> | BROWN_400                                                             | <span style="white-space:nowrap">Brown (400)</span>   | #8D6E63 | 141,110,99  | 16,30,55    |
| <p style="background-color: #795548">　　　</p> | <span style="white-space:nowrap">BROWN_500 / BROWN</span>             | <span style="white-space:nowrap">Brown (500)</span>   | #795548 | 121,85,72   | 16,40,47    |
| <p style="background-color: #6D4C41">　　　</p> | BROWN_600                                                             | <span style="white-space:nowrap">Brown (600)</span>   | #6D4C41 | 109,76,65   | 15,40,43    |
| <p style="background-color: #5D4037">　　　</p> | BROWN_700                                                             | <span style="white-space:nowrap">Brown (700)</span>   | #5D4037 | 93,64,55    | 14,41,36    |
| <p style="background-color: #4E342E">　　　</p> | BROWN_800                                                             | <span style="white-space:nowrap">Brown (800)</span>   | #4E342E | 78,52,46    | 11,41,31    |
| <p style="background-color: #3E2723">　　　</p> | BROWN_900                                                             | <span style="white-space:nowrap">Brown (900)</span>   | #3E2723 | 62,39,35    | 9,44,24     |
| <p style="background-color: #FAFAFA">　　　</p> | GREY_50                                                               | <span style="white-space:nowrap">Grey (50)</span>    | #FAFAFA | 250,250,250 | 0,0,98      |
| <p style="background-color: #F5F5F5">　　　</p> | GREY_100                                                              | <span style="white-space:nowrap">Grey (100)</span>   | #F5F5F5 | 245,245,245 | 0,0,96      |
| <p style="background-color: #EEEEEE">　　　</p> | GREY_200                                                              | <span style="white-space:nowrap">Grey (200)</span>   | #EEEEEE | 238,238,238 | 0,0,93      |
| <p style="background-color: #E0E0E0">　　　</p> | GREY_300                                                              | <span style="white-space:nowrap">Grey (300)</span>   | #E0E0E0 | 224,224,224 | 0,0,88      |
| <p style="background-color: #BDBDBD">　　　</p> | GREY_400                                                              | <span style="white-space:nowrap">Grey (400)</span>   | #BDBDBD | 189,189,189 | 0,0,74      |
| <p style="background-color: #9E9E9E">　　　</p> | <span style="white-space:nowrap">GREY_500 / GREY</span>               | <span style="white-space:nowrap">Grey (500)</span>   | #9E9E9E | 158,158,158 | 0,0,62      |
| <p style="background-color: #757575">　　　</p> | GREY_600                                                              | <span style="white-space:nowrap">Grey (600)</span>   | #757575 | 117,117,117 | 0,0,46      |
| <p style="background-color: #616161">　　　</p> | GREY_700                                                              | <span style="white-space:nowrap">Grey (700)</span>   | #616161 | 97,97,97    | 0,0,38      |
| <p style="background-color: #424242">　　　</p> | GREY_800                                                              | <span style="white-space:nowrap">Grey (800)</span>   | #424242 | 66,66,66    | 0,0,26      |
| <p style="background-color: #212121">　　　</p> | GREY_900                                                              | <span style="white-space:nowrap">Grey (900)</span>   | #212121 | 33,33,33    | 0,0,13      |
| <p style="background-color: #000000">　　　</p> | <span style="white-space:nowrap">BLACK_1000 / BLACK</span>            | <span style="white-space:nowrap">Black</span>         | #000000 | 0,0,0       | 0,0,0       |
| <p style="background-color: #FFFFFF">　　　</p> | <span style="white-space:nowrap">WHITE_1000 / WHITE</span>            | <span style="white-space:nowrap">White</span>         | #FFFFFF | 255,255,255 | 0,0,100     |
| <p style="background-color: #ECEFF1">　　　</p> | BLUE_GREY_50                                                          | <span style="white-space:nowrap">Blue Grey (50)</span>   | #ECEFF1 | 236,239,241 | 204,2,95    |
| <p style="background-color: #CFD8DC">　　　</p> | BLUE_GREY_100                                                         | <span style="white-space:nowrap">Blue Grey (100)</span>  | #CFD8DC | 207,216,220 | 198,6,86    |
| <p style="background-color: #B0BBC5">　　　</p> | BLUE_GREY_200                                                         | <span style="white-space:nowrap">Blue Grey (200)</span>  | #B0BBC5 | 176,187,197 | 209,11,77   |
| <p style="background-color: #90A4AE">　　　</p> | BLUE_GREY_300                                                         | <span style="white-space:nowrap">Blue Grey (300)</span>  | #90A4AE | 144,164,174 | 200,17,68   |
| <p style="background-color: #78909C">　　　</p> | BLUE_GREY_400                                                         | <span style="white-space:nowrap">Blue Grey (400)</span>  | #78909C | 120,144,156 | 200,23,61   |
| <p style="background-color: #607D8B">　　　</p> | <span style="white-space:nowrap">BLUE_GREY_500 / BLUE_GREY</span>     | <span style="white-space:nowrap">Blue Grey (500)</span>  | #607D8B | 96,125,139  | 200,31,55   |
| <p style="background-color: #546E7A">　　　</p> | BLUE_GREY_600                                                         | <span style="white-space:nowrap">Blue Grey (600)</span>  | #546E7A | 84,110,122  | 199,31,48   |
| <p style="background-color: #455A64">　　　</p> | BLUE_GREY_700                                                         | <span style="white-space:nowrap">Blue Grey (700)</span>  | #455A64 | 69,90,100   | 199,31,39   |
| <p style="background-color: #37474F">　　　</p> | BLUE_GREY_800                                                         | <span style="white-space:nowrap">Blue Grey (800)</span>  | #37474F | 55,71,79    | 200,30,31   |
| <p style="background-color: #263238">　　　</p> | BLUE_GREY_900                                                         | <span style="white-space:nowrap">Blue Grey (900)</span>  | #263238 | 38,50,56    | 200,32,22   |

## Abbreviated Color List

Three-digit shorthand Hex color codes are supported when each of the R / G / B components follows a repeated-digit pattern, such as `#663399`, `#CCFF00`, `#888888`, etc.

You can use [colors.toHex(color, 3)](color#tohexcolor-length) to convert from `#RRGGBB` to `#RGB`:

```js
colors.toHex(colors.GRAY, 3); // #888
colors.toHex(colors.css.REBECCA_PURPLE, 3); // #639
colors.toHex(colors.web.BURNT_ORANGE, 3); // #C50

/* PURPLE cannot be simplified, because neither the R nor B component of #800080 follows the repeated-digit pattern. */
colors.toHex(colors.PURPLE, 3); /* Throws an exception. */
```

The following table summarizes all colors from the above lists that support this shorthand conversion:

| Namespace    |                      Color                      | Variable Name                                                                | Color Name                                               | Hex Code  | RGB         | HSV         |
|----------|:--------------------------------------------:|--------------------------------------------------------------------|----------------------------------------------------|---------|-------------|-------------|
| android  | <p style="background-color: #000000">　　　</p> | BLACK                                                              | <span style="white-space:nowrap">Black</span>          | #000000 | 0,0,0       | 0,0,0       |
| android  | <p style="background-color: #0000FF">　　　</p> | BLUE                                                               | <span style="white-space:nowrap">Blue</span>          | #0000FF | 0,0,255     | 240,100,100 |
| android  | <p style="background-color: #00FFFF">　　　</p> | <span style="white-space:nowrap">CYAN / AQUA</span>                | <span style="white-space:nowrap">Cyan</span>          | #00FFFF | 0,255,255   | 180,100,100 |
| android  | <p style="background-color: #444444">　　　</p> | DARK_GRAY<br/>DARK_GREY<br/>DKGRAY                                 | <span style="white-space:nowrap">Dark Gray</span>         | #444444 | 68,68,68    | 0,0,27      |
| android  | <p style="background-color: #888888">　　　</p> | GRAY<br/>GREY                                                      | <span style="white-space:nowrap">Gray</span>          | #888888 | 136,136,136 | 0,0,53      |
| android  | <p style="background-color: #00FF00">　　　</p> | <span style="white-space:nowrap">GREEN / LIME</span>               | <span style="white-space:nowrap">Green</span>          | #00FF00 | 0,255,0     | 120,100,100 |
| android  | <p style="background-color: #CCCCCC">　　　</p> | LIGHT_GRAY<br/>LIGHT_GREY<br/>LTGRAY                               | <span style="white-space:nowrap">Light Gray</span>         | #CCCCCC | 204,204,204 | 0,0,80      |
| android  | <p style="background-color: #FF00FF">　　　</p> | <span style="white-space:nowrap">MAGENTA / FUCHSIA</span>          | <span style="white-space:nowrap">Magenta / Fuchsia</span>    | #FF00FF | 255,0,255   | 300,100,100 |
| android  | <p style="background-color: #FF0000">　　　</p> | RED                                                                | <span style="white-space:nowrap">Red</span>          | #FF0000 | 255,0,0     | 0,100,100   |
| android  | <p style="background-color: #FFFFFF">　　　</p> | WHITE                                                              | <span style="white-space:nowrap">White</span>          | #FFFFFF | 255,255,255 | 0,0,100     |
| android  | <p style="background-color: #FFFF00">　　　</p> | YELLOW                                                             | <span style="white-space:nowrap">Yellow</span>          | #FFFF00 | 255,255,0   | 60,100,100  |
| css      | <p style="background-color: #778899">　　　</p> | LIGHT_SLATE_GRAY<br/>LIGHT_SLATE_GREY                              | <span style="white-space:nowrap">Light Slate Gray</span>        | #778899 | 119,136,153 | 210,22,60   |
| css      | <p style="background-color: #663399">　　　</p> | REBECCA_PURPLE                                                     | <span style="white-space:nowrap">Rebecca Purple</span>       | #663399 | 102,51,153  | 270,67,60   |
| web      | <p style="background-color: #9966CC">　　　</p> | AMETHYST                                                           | <span style="white-space:nowrap">Amethyst</span>        | #9966CC | 153,102,204 | 270,50,80   |
| web      | <p style="background-color: #66FF00">　　　</p> | BRIGHT_GREEN                                                       | <span style="white-space:nowrap">Bright Green / Vivid Green</span>    | #66FF00 | 102,255,0   | 96,100,100  |
| web      | <p style="background-color: #CC5500">　　　</p> | BURNT_ORANGE                                                       | <span style="white-space:nowrap">Burnt Orange</span>         | #CC5500 | 204,85,0    | 25,100,80   |
| web      | <p style="background-color: #FFFF99">　　　</p> | CHAMPAGNE_YELLOW                                                   | <span style="white-space:nowrap">Champagne Yellow</span>        | #FFFF99 | 255,255,153 | 60,40,100   |
| web      | <p style="background-color: #003399">　　　</p> | DARK_POWDER_BLUE                                                   | <span style="white-space:nowrap">Dark Powder Blue</span>        | #003399 | 0,51,153    | 220,100,60  |
| web      | <p style="background-color: #CCCCFF">　　　</p> | <span style="white-space:nowrap">LAVENDER_BLUE / PERIWINKLE</span> | <span style="white-space:nowrap">Lavender Blue / Periwinkle</span> | #CCCCFF | 204,204,255 | 240,20,100  |
| web      | <p style="background-color: #CCFF00">　　　</p> | <span style="white-space:nowrap">LIME / LIGHT_LIME</span>          | <span style="white-space:nowrap">Lime / Light Lime</span> | #CCFF00 | 204,255,0   | 72,100,100  |
| web      | <p style="background-color: #FF9900">　　　</p> | MARIGOLD                                                           | <span style="white-space:nowrap">Marigold</span>       | #FF9900 | 255,153,0   | 36,100,100  |
| web      | <p style="background-color: #CC7722">　　　</p> | OCHER                                                              | <span style="white-space:nowrap">Ocher</span>          | #CC7722 | 204,119,34  | 30,83,80    |
| web      | <p style="background-color: #FF66CC">　　　</p> | ROSE_PINK                                                          | <span style="white-space:nowrap">Rose Pink</span>       | #FF66CC | 255,102,204 | 320,60,100  |
| web      | <p style="background-color: #FFCC00">　　　</p> | TANGERINE_YELLOW                                                   | <span style="white-space:nowrap">Tangerine Yellow</span>         | #FFCC00 | 255,204,0   | 48,100,100  |
| web      | <p style="background-color: #0033FF">　　　</p> | ULTRAMARINE                                                        | <span style="white-space:nowrap">Ultramarine</span>       | #0033FF | 0,51,255    | 228,100,100 |
| material | <p style="background-color: #AA00FF">　　　</p> | PURPLE_A700                                                        | <span style="white-space:nowrap">Purple (A700)</span>   | #AA00FF | 170,0,255   | 280,100,100 |
| material | <p style="background-color: #EEEEEE">　　　</p> | GREY_200                                                           | <span style="white-space:nowrap">Grey (200)</span>    | #EEEEEE | 238,238,238 | 0,0,93      |

## Color Name Conflicts

When using a [Color Name (ColorName)](dataTypes#colorname) as a parameter, the same name may appear in multiple color lists. For example, `CYAN` exists in all lists, and the `CYAN` in the [Material Color List](#material-color-list) is different from the `CYAN` in other lists.

To avoid such conflicts, colors are looked up and used according to the following namespace priority:

```text
android > css > web > material
```

Therefore, the color name `CYAN` is equivalent to `colors.android.CYAN` (not `colors.web.CYAN`);  
the color name `ORANGE` is equivalent to `colors.css.ORANGE` (not `colors.material.ORANGE`).

The table below lists all colors that have conflicts. The "Decisive" column indicates which row's color will be used in case of a conflict:

| Decisive | Namespace    |                      Color                      | Variable Name   | Color Name                                               | Hex Code  | RGB         | HSV         |
|:---:|----------|:--------------------------------------------:|--------------|----------------------------------------------------|---------|-------------|-------------|
|  √  | android  | <p style="background-color: #0000FF">　　　</p> | BLUE         | <span style="white-space:nowrap">Blue</span>          | #0000FF | 0,0,255     | 240,100,100 |
|     | material | <p style="background-color: #2196F3">　　　</p> |              | <span style="white-space:nowrap">Blue (500)</span>    | #2196F3 | 33,150,243  | 207,86,95   |
|  √  | android  | <p style="background-color: #00FFFF">　　　</p> | CYAN         | <span style="white-space:nowrap">Cyan</span>          | #00FFFF | 0,255,255   | 180,100,100 |
|     | css      | <p style="background-color: #00FFFF">　　　</p> |              | <span style="white-space:nowrap">Cyan</span>          | #00FFFF | 0,255,255   | 180,100,100 |
|     | web      | <p style="background-color: #00FFFF">　　　</p> |              | <span style="white-space:nowrap">Cyan</span>          | #00FFFF | 0,255,255   | 180,100,100 |
|     | material | <p style="background-color: #00BCD4">　　　</p> |              | <span style="white-space:nowrap">Cyan (500)</span>    | #00BCD4 | 0,188,212   | 187,100,83  |
|  √  | android  | <p style="background-color: #00FFFF">　　　</p> | AQUA         | <span style="white-space:nowrap">Cyan</span>          | #00FFFF | 0,255,255   | 180,100,100 |
|     | css      | <p style="background-color: #00FFFF">　　　</p> |              | <span style="white-space:nowrap">Cyan</span>          | #00FFFF | 0,255,255   | 180,100,100 |
|     | web      | <p style="background-color: #AFDFE4">　　　</p> |              | <span style="white-space:nowrap">Aqua</span>          | #AFDFE4 | 175,223,228 | 186,23,89   |
|  √  | android  | <p style="background-color: #444444">　　　</p> | DARK_GRAY    | <span style="white-space:nowrap">Dark Gray</span>         | #444444 | 68,68,68    | 0,0,27      |
|     | css      | <p style="background-color: #A9A9A9">　　　</p> |              | <span style="white-space:nowrap">Dark Gray</span>         | #A9A9A9 | 169,169,169 | 0,0,66      |
|     | web      | <p style="background-color: #A9A9A9">　　　</p> |              | <span style="white-space:nowrap">Dark Gray</span>         | #A9A9A9 | 169,169,169 | 0,0,66      |
|  √  | android  | <p style="background-color: #444444">　　　</p> | DARK_GREY    | <span style="white-space:nowrap">Dark Gray</span>         | #444444 | 68,68,68    | 0,0,27      |
|     | css      | <p style="background-color: #A9A9A9">　　　</p> |              | <span style="white-space:nowrap">Dark Gray</span>         | #A9A9A9 | 169,169,169 | 0,0,66      |
|  √  | android  | <p style="background-color: #888888">　　　</p> | GRAY         | <span style="white-space:nowrap">Gray</span>          | #888888 | 136,136,136 | 0,0,53      |
|     | css      | <p style="background-color: #808080">　　　</p> |              | <span style="white-space:nowrap">Gray</span>          | #808080 | 128,128,128 | 0,0,50      |
|     | web      | <p style="background-color: #808080">　　　</p> |              | <span style="white-space:nowrap">Gray</span>          | #808080 | 128,128,128 | 0,0,50      |
|  √  | android  | <p style="background-color: #888888">　　　</p> | GREY         | <span style="white-space:nowrap">Gray</span>          | #888888 | 136,136,136 | 0,0,53      |
|     | css      | <p style="background-color: #808080">　　　</p> |              | <span style="white-space:nowrap">Gray</span>          | #808080 | 128,128,128 | 0,0,50      |
|     | material | <p style="background-color: #9E9E9E">　　　</p> |              | <span style="white-space:nowrap">Grey (500)</span>    | #9E9E9E | 158,158,158 | 0,0,62      |
|  √  | android  | <p style="background-color: #00FF00">　　　</p> | GREEN        | <span style="white-space:nowrap">Green</span>          | #00FF00 | 0,255,0     | 120,100,100 |
|     | css      | <p style="background-color: #008000">　　　</p> |              | <span style="white-space:nowrap">Green</span>          | #008000 | 0,128,0     | 120,100,50  |
|     | web      | <p style="background-color: #008000">　　　</p> |              | <span style="white-space:nowrap">Green</span>          | #008000 | 0,128,0     | 120,100,50  |
|     | material | <p style="background-color: #4CAF50">　　　</p> |              | <span style="white-space:nowrap">Green (500)</span>    | #4CAF50 | 76,175,80   | 122,57,69   |
|  √  | android  | <p style="background-color: #00FF00">　　　</p> | LIME         | <span style="white-space:nowrap">Green</span>          | #00FF00 | 0,255,0     | 120,100,100 |
|     | css      | <p style="background-color: #00FF00">　　　</p> |              | <span style="white-space:nowrap">Lime / Fresh Green</span>    | #00FF00 | 0,255,0     | 120,100,100 |
|     | web      | <p style="background-color: #CCFF00">　　　</p> |              | <span style="white-space:nowrap">Lime / Light Lime</span> | #CCFF00 | 204,255,0   | 72,100,100  |
|     | material | <p style="background-color: #CDDC39">　　　</p> |              | <span style="white-space:nowrap">Lime (500)</span>   | #CDDC39 | 205,220,57  | 66,74,86    |
|  √  | android  | <p style="background-color: #CCCCCC">　　　</p> | LIGHT_GRAY   | <span style="white-space:nowrap">Light Gray</span>         | #CCCCCC | 204,204,204 | 0,0,80      |
|     | css      | <p style="background-color: #D3D3D3">　　　</p> |              | <span style="white-space:nowrap">Light Gray</span>         | #D3D3D3 | 211,211,211 | 0,0,83      |
|     | web      | <p style="background-color: #D3D3D3">　　　</p> |              | <span style="white-space:nowrap">Light Gray</span>         | #D3D3D3 | 211,211,211 | 0,0,83      |
|  √  | android  | <p style="background-color: #CCCCCC">　　　</p> | LIGHT_GREY   | <span style="white-space:nowrap">Light Gray</span>         | #CCCCCC | 204,204,204 | 0,0,80      |
|     | css      | <p style="background-color: #D3D3D3">　　　</p> |              | <span style="white-space:nowrap">Light Gray</span>         | #D3D3D3 | 211,211,211 | 0,0,83      |
|  √  | android  | <p style="background-color: #FF00FF">　　　</p> | FUCHSIA      | <span style="white-space:nowrap">Magenta / Fuchsia</span>    | #FF00FF | 255,0,255   | 300,100,100 |
|     | css      | <p style="background-color: #FF00FF">　　　</p> |              | <span style="white-space:nowrap">Magenta / Fuchsia</span>    | #FF00FF | 255,0,255   | 300,100,100 |
|     | web      | <p style="background-color: #F400A1">　　　</p> |              | <span style="white-space:nowrap">Fuchsia / Magenta Red</span>         | #F400A1 | 244,0,161   | 320,100,96  |
|  √  | android  | <p style="background-color: #800080">　　　</p> | PURPLE       | <span style="white-space:nowrap">Purple</span>          | #800080 | 128,0,128   | 300,100,50  |
|     | css      | <p style="background-color: #9C27B0">　　　</p> |              | <span style="white-space:nowrap">Purple (500)</span>    | #9C27B0 | 156,39,176  | 291,78,69   |
|     | web      | <p style="background-color: #6A0DAD">　　　</p> |              | <span style="white-space:nowrap">Purple</span>          | #6A0DAD | 106,13,173  | 275,92,68   |
|  √  | android  | <p style="background-color: #FF0000">　　　</p> | RED          | <span style="white-space:nowrap">Red</span>          | #FF0000 | 255,0,0     | 0,100,100   |
|     | css      | <p style="background-color: #FF0000">　　　</p> |              | <span style="white-space:nowrap">Red</span>          | #FF0000 | 255,0,0     | 0,100,100   |
|     | web      | <p style="background-color: #FF0000">　　　</p> |              | <span style="white-space:nowrap">Red</span>          | #FF0000 | 255,0,0     | 0,100,100   |
|     | material | <p style="background-color: #F44336">　　　</p> |              | <span style="white-space:nowrap">Red (500)</span>    | #F44336 | 244,67,54   | 4,78,96     |
|  √  | android  | <p style="background-color: #008080">　　　</p> | TEAL         | <span style="white-space:nowrap">Teal</span>    | #008080 | 0,128,128   | 180,100,50  |
|     | css      | <p style="background-color: #008080">　　　</p> |              | <span style="white-space:nowrap">Teal</span>    | #008080 | 0,128,128   | 180,100,50  |
|     | web      | <p style="background-color: #008080">　　　</p> |              | <span style="white-space:nowrap">Teal</span>    | #008080 | 0,128,128   | 180,100,50  |
|     | material | <p style="background-color: #009688">　　　</p> |              | <span style="white-space:nowrap">Teal (500)</span>   | #009688 | 0,150,136   | 174,100,59  |
|  √  | android  | <p style="background-color: #FFFF00">　　　</p> | YELLOW       | <span style="white-space:nowrap">Yellow</span>          | #FFFF00 | 255,255,0   | 60,100,100  |
|     | css      | <p style="background-color: #FFFF00">　　　</p> |              | <span style="white-space:nowrap">Yellow</span>          | #FFFF00 | 255,255,0   | 60,100,100  |
|     | web      | <p style="background-color: #FFFF00">　　　</p> |              | <span style="white-space:nowrap">Yellow</span>          | #FFFF00 | 255,255,0   | 60,100,100  |
|     | material | <p style="background-color: #FFEB3B">　　　</p> |              | <span style="white-space:nowrap">Yellow (500)</span>    | #FFEB3B | 255,235,59  | 54,77,100   |
|  √  | css      | <p style="background-color: #FFC0CB">　　　</p> | PINK         | <span style="white-space:nowrap">Pink</span>         | #FFC0CB | 255,192,203 | 350,25,100  |
|     | web      | <p style="background-color: #FFC0CB">　　　</p> |              | <span style="white-space:nowrap">Pink</span>         | #FFC0CB | 255,192,203 | 350,25,100  |
|     | material | <p style="background-color: #E91E63">　　　</p> |              | <span style="white-space:nowrap">Pink (500)</span>   | #E91E63 | 233,30,99   | 340,87,91   |
|  √  | css      | <p style="background-color: #4B0082">　　　</p> | INDIGO       | <span style="white-space:nowrap">Indigo</span>          | #4B0082 | 75,0,130    | 	275,100,51 |
|     | web      | <p style="background-color: #4B0080">　　　</p> |              | <span style="white-space:nowrap">Indigo</span>          | #4B0080 | 75,0,128    | 275,100,50  |
|     | material | <p style="background-color: #3F51B5">　　　</p> |              | <span style="white-space:nowrap">Indigo (500)</span>   | #3F51B5 | 63,81,181   | 231,65,71   |
|  √  | css      | <p style="background-color: #ADD8E6">　　　</p> | LIGHT_BLUE   | <span style="white-space:nowrap">Light Blue</span>         | #ADD8E6 | 173,216,230 | 195,25,90   |
|     | web      | <p style="background-color: #ADD8E6">　　　</p> |              | <span style="white-space:nowrap">Light Blue</span>         | #ADD8E6 | 173,216,230 | 195,25,90   |
|     | material | <p style="background-color: #03A9F4">　　　</p> |              | <span style="white-space:nowrap">Light Blue (500)</span>   | #03A9F4 | 3,169,244   | 199,99,96   |
|  √  | css      | <p style="background-color: #90EE90">　　　</p> | LIGHT_GREEN  | <span style="white-space:nowrap">Light Green</span>         | #90EE90 | 144,238,144 | 120,39,93   |
|     | web      | <p style="background-color: #90EE90">　　　</p> |              | <span style="white-space:nowrap">Light Green</span>         | #90EE90 | 144,238,144 | 120,39,93   |
|     | material | <p style="background-color: #8BC34A">　　　</p> |              | <span style="white-space:nowrap">Light Green (500)</span>   | #8BC34A | 139,195,74  | 88,62,76    |
|  √  | web      | <p style="background-color: #FFBF00">　　　</p> | AMBER        | <span style="white-space:nowrap">Amber</span>         | #FFBF00 | 255,191,0   | 45,100,100  |
|     | material | <p style="background-color: #FFC107">　　　</p> |              | <span style="white-space:nowrap">Amber (500)</span>   | #FFC107 | 255,193,7   | 45,97,100   |
|  √  | css      | <p style="background-color: #FFA500">　　　</p> | ORANGE       | <span style="white-space:nowrap">Orange</span>          | #FFA500 | 255,165,0   | 39,100,100  |
|     | web      | <p style="background-color: #FFA500">　　　</p> |              | <span style="white-space:nowrap">Orange</span>          | #FFA500 | 255,165,0   | 39,100,100  |
|     | material | <p style="background-color: #FF9800">　　　</p> |              | <span style="white-space:nowrap">Orange (500)</span>    | #FF9800 | 255,152,0   | 36,100,100  |
|  √  | css      | <p style="background-color: #A52A2A">　　　</p> | BROWN        | <span style="white-space:nowrap">Brown</span>          | #A52A2A | 165,42,42   | 0,75,65     |
|     | web      | <p style="background-color: #A52A2A">　　　</p> |              | <span style="white-space:nowrap">Brown</span>          | #A52A2A | 165,42,42   | 0,75,65     |
|     | material | <p style="background-color: #795548">　　　</p> |              | <span style="white-space:nowrap">Brown (500)</span>    | #795548 | 121,85,72   | 16,40,47    |
|  √  | css      | <p style="background-color: #F0FFFF">　　　</p> | AZURE        | <span style="white-space:nowrap">Azure</span>         | #F0FFFF | 240,255,255 | 210,100,100 |
|     | web      | <p style="background-color: #007FFF">　　　</p> |              | <span style="white-space:nowrap">Azure / Azure Blue</span>    | #007FFF | 0,127,255   | 210,100,100 |
|  √  | css      | <p style="background-color: #F0E68C">　　　</p> | KHAKI        | <span style="white-space:nowrap">Khaki</span>         | #F0E68C | 240,230,140 | 54,42,94    |
|     | web      | <p style="background-color: #996B1F">　　　</p> |              | <span style="white-space:nowrap">Khaki</span>         | #996B1F | 153,107,31  | 37,80,60    |
|  √  | css      | <p style="background-color: #E6E6FA">　　　</p> | LAVENDER     | <span style="white-space:nowrap">Lavender</span>        | #E6E6FA | 230,230,250 | 240,8,98    |
|     | web      | <p style="background-color: #B57EDC">　　　</p> |              | <span style="white-space:nowrap">Lavender</span>       | #B57EDC | 181,126,220 | 275,43,86   |
|  √  | css      | <p style="background-color: #00FF7F">　　　</p> | SPRING_GREEN | <span style="white-space:nowrap">Spring Green</span>         | #00FF7F | 0,255,127   | 150,100,100 |
|     | web      | <p style="background-color: #00FF80">　　　</p> |              | <span style="white-space:nowrap">Spring Green</span>         | #00FF80 | 0,255,128   | 150,100,100 |
|  √  | css      | <p style="background-color: #40E0D0">　　　</p> | TURQUOISE    | <span style="white-space:nowrap">Turquoise</span>         | #40E0D0 | 64,224,208  | 174,71,88   |
|     | web      | <p style="background-color: #30D5C8">　　　</p> |              | <span style="white-space:nowrap">Turquoise</span>   | #30D5C8 | 48,213,200  | 210,100,100 |
|  √  | css      | <p style="background-color: #EE82EE">　　　</p> | VIOLET       | <span style="white-space:nowrap">Violet</span>        | #EE82EE | 238,130,238 | 300,45,93   |
|     | web      | <p style="background-color: #8000FF">　　　</p> |              | <span style="white-space:nowrap">Violet</span>         | #8000FF | 128,0,255   | 270,100,100 |

## Fused Color List

If you want to access a color constant without caring which color list the name belongs to, you can use the color name directly.

For example, for `Orange`:

```js
/* Color list access method. */
colors.css.ORANGE;

/* Color name access method (as a property of the colors object). */
colors.ORANGE;

/* Color name access method (as a string parameter). */
colors.toInt('orange');
```

In fact, there is also an `ORANGE` color in the [Material Color List](#material-color-list):

```js
colors.material.ORANGE;
```

For colors like `ORANGE` that have mapping conflicts, the following namespace priority is followed:

```text
android > css > web > material
```

It can be seen that the `css` namespace has higher priority than `material`, so `colors.ORANGE` is equivalent to `colors.css.ORANGE`. See the [Color Name Conflicts](#color-name-conflicts) section for details.

All color lists are merged according to the above namespace priority, and all conflicting items are removed to obtain a new fused list:

| Namespace    | Color                                             | Variable Name                 | Color Name                                              | Hex Code    | RGB            | HSV            |
|----------|------------------------------------------------|----------------------------|-----------------------------------------------------|-----------|----------------|----------------|
| css      | <p style="background-color: #F0F8FF">　　　</p>   | ALICE_BLUE                 | <span style="white-space:nowrap">Alice Blue</span>        | #F0F8FF   | 240,248,255    | 208,6,100      |
| web      | <p style="background-color: #E32636">　　　</p>   | ALIZARIN_CRIMSON           | <span style="white-space:nowrap">Alizarin Crimson / Deep Alizarin Crimson</span>    | #E32636   | 227,38,54      | 355,83,89      |
| web      | <p style="background-color: #FFBF00">　　　</p>   | AMBER                      | <span style="white-space:nowrap">Amber</span>          | #FFBF00   | 255,191,0      | 45,100,100     |
| material | <p style="background-color: #FFF8E1">　　　</p>   | AMBER_50                   | <span style="white-space:nowrap">Amber (50)</span>     | #FFF8E1   | 255,248,225    | 46,12,100      |
| material | <p style="background-color: #FFECB3">　　　</p>   | AMBER_100                  | <span style="white-space:nowrap">Amber (100)</span>    | #FFECB3   | 255,236,179    | 45,30,100      |
| material | <p style="background-color: #FFE082">　　　</p>   | AMBER_200                  | <span style="white-space:nowrap">Amber (200)</span>    | #FFE082   | 255,224,130    | 45,49,100      |
| material | <p style="background-color: #FFD54F">　　　</p>   | AMBER_300                  | <span style="white-space:nowrap">Amber (300)</span>    | #FFD54F   | 255,213,79     | 46,69,100      |
| material | <p style="background-color: #FFCA28">　　　</p>   | AMBER_400                  | <span style="white-space:nowrap">Amber (400)</span>    | #FFCA28   | 255,202,40     | 45,84,100      |
| material | <p style="background-color: #FFC107">　　　</p>   | AMBER_500                  | <span style="white-space:nowrap">Amber (500)</span>    | #FFC107   | 255,193,7      | 45,97,100      |
| material | <p style="background-color: #FFB300">　　　</p>   | AMBER_600                  | <span style="white-space:nowrap">Amber (600)</span>    | #FFB300   | 255,179,0      | 42,100,100     |
| material | <p style="background-color: #FFA000">　　　</p>   | AMBER_700                  | <span style="white-space:nowrap">Amber (700)</span>    | #FFA000   | 255,160,0      | 38,100,100     |
| material | <p style="background-color: #FF8F00">　　　</p>   | AMBER_800                  | <span style="white-space:nowrap">Amber (800)</span>    | #FF8F00   | 255,143,0      | 34,100,100     |
| material | <p style="background-color: #FF6F00">　　　</p>   | AMBER_900                  | <span style="white-space:nowrap">Amber (900)</span>    | #FF6F00   | 255,111,0      | 26,100,100     |
| material | <p style="background-color: #FFE57F">　　　</p>   | AMBER_A100                 | <span style="white-space:nowrap">Amber (A100)</span>   | #FFE57F   | 255,229,127    | 48,50,100      |
| material | <p style="background-color: #FFD740">　　　</p>   | AMBER_A200                 | <span style="white-space:nowrap">Amber (A200)</span>   | #FFD740   | 255,215,64     | 47,75,100      |
| material | <p style="background-color: #FFC400">　　　</p>   | AMBER_A400                 | <span style="white-space:nowrap">Amber (A400)</span>   | #FFC400   | 255,196,0      | 46,100,100     |
| material | <p style="background-color: #FFAB00">　　　</p>   | AMBER_A700                 | <span style="white-space:nowrap">Amber (A700)</span>   | #FFAB00   | 255,171,0      | 40,100,100     |
| web      | <p style="background-color: #9966CC">　　　</p>   | AMETHYST                   | <span style="white-space:nowrap">Amethyst</span>         | #9966CC   | 153,102,204    | 270,50,80      |
| css      | <p style="background-color: #FAEBD7">　　　</p>   | ANTIQUE_WHITE              | <span style="white-space:nowrap">Antique White</span>         | #FAEBD7   | 250,235,215    | 34,14,98       |
| web      | <p style="background-color: #8CE600">　　　</p>   | APPLE_GREEN                | <span style="white-space:nowrap">Apple Green</span>         | #8CE600   | 140,230,0      | 83,100,90      |
| web      | <p style="background-color: #E69966">　　　</p>   | APRICOT                    | <span style="white-space:nowrap">Apricot</span>          | #E69966   | 230,153,102    | 24,56,90       |
| android  | <p style="background-color: #00FFFF">　　　</p>   | AQUA                       | <span style="white-space:nowrap">Cyan</span>           | #00FFFF   | 0,255,255      | 180,100,100    |
| css      | <p style="background-color: #7FFFD4">　　　</p>   | AQUAMARINE                 | <span style="white-space:nowrap">Aquamarine</span>     | #7FFFD4   | 127,255,212    | 160,50,100     |
| web      | <p style="background-color: #66FFE6">　　　</p>   | AQUA_BLUE                  | <span style="white-space:nowrap">Aqua Blue</span>          | #66FFE6   | 102,255,230    | 170,60,100     |
| css      | <p style="background-color: #F0FFFF">　　　</p>   | AZURE                      | <span style="white-space:nowrap">Azure</span>          | #F0FFFF   | 240,255,255    | 210,100,100    |
| web      | <p style="background-color: #89CFF0">　　　</p>   | BABY_BLUE                  | <span style="white-space:nowrap">Baby Blue</span>          | #89CFF0   | 137,207,240    | 199,43,94      |
| web      | <p style="background-color: #FFD9E6">　　　</p>   | BABY_PINK                  | <span style="white-space:nowrap">Baby Pink</span>         | #FFD9E6   | 255,217,230    | 339,15,100     |
| css      | <p style="background-color: #F5F5DC">　　　</p>   | BEIGE                      | <span style="white-space:nowrap">Beige</span>          | #F5F5DC   | 245,245,220    | 60,10,96       |
| css      | <p style="background-color: #FFE4C4">　　　</p>   | BISQUE                     | <span style="white-space:nowrap">Bisque</span>         | #FFE4C4   | 255,228,196    | 33,23,100      |
| android  | <p style="background-color: #000000">　　　</p>   | BLACK                      | <span style="white-space:nowrap">Black</span>           | #000000   | 0,0,0          | 0,0,0          |
| material | <p style="background-color: #000000">　　　</p>   | BLACK_1000                 | <span style="white-space:nowrap">Black</span>           | #000000   | 0,0,0          | 0,0,0          |
| css      | <p style="background-color: #FFEBCD">　　　</p>   | BLANCHED_ALMOND            | <span style="white-space:nowrap">Blanched Almond</span>         | #FFEBCD   | 255,235,205    | 36,20,100      |
| android  | <p style="background-color: #0000FF">　　　</p>   | BLUE                       | <span style="white-space:nowrap">Blue</span>           | #0000FF   | 0,0,255        | 240,100,100    |
| material | <p style="background-color: #E3F2FD">　　　</p>   | BLUE_50                    | <span style="white-space:nowrap">Blue (50)</span>      | #E3F2FD   | 227,242,253    | 205,10,99      |
| material | <p style="background-color: #BBDEFB">　　　</p>   | BLUE_100                   | <span style="white-space:nowrap">Blue (100)</span>     | #BBDEFB   | 187,222,251    | 207,25,98      |
| material | <p style="background-color: #90CAF9">　　　</p>   | BLUE_200                   | <span style="white-space:nowrap">Blue (200)</span>     | #90CAF9   | 144,202,249    | 207,42,98      |
| material | <p style="background-color: #64B5F6">　　　</p>   | BLUE_300                   | <span style="white-space:nowrap">Blue (300)</span>     | #64B5F6   | 100,181,246    | 207,59,96      |
| material | <p style="background-color: #42A5F5">　　　</p>   | BLUE_400                   | <span style="white-space:nowrap">Blue (400)</span>     | #42A5F5   | 66,165,245     | 207,73,96      |
| material | <p style="background-color: #2196F3">　　　</p>   | BLUE_500                   | <span style="white-space:nowrap">Blue (500)</span>     | #2196F3   | 33,150,243     | 207,86,95      |
| material | <p style="background-color: #1E88E5">　　　</p>   | BLUE_600                   | <span style="white-space:nowrap">Blue (600)</span>     | #1E88E5   | 30,136,229     | 208,87,90      |
| material | <p style="background-color: #1976D2">　　　</p>   | BLUE_700                   | <span style="white-space:nowrap">Blue (700)</span>     | #1976D2   | 25,118,210     | 210,88,82      |
| material | <p style="background-color: #1565C0">　　　</p>   | BLUE_800                   | <span style="white-space:nowrap">Blue (800)</span>     | #1565C0   | 21,101,192     | 212,89,75      |
| material | <p style="background-color: #0D47A1">　　　</p>   | BLUE_900                   | <span style="white-space:nowrap">Blue (900)</span>     | #0D47A1   | 13,71,161      | 216,92,63      |
| material | <p style="background-color: #82B1FF">　　　</p>   | BLUE_A100                  | <span style="white-space:nowrap">Blue (A100)</span>    | #82B1FF   | 130,177,255    | 217,49,100     |
| material | <p style="background-color: #448AFF">　　　</p>   | BLUE_A200                  | <span style="white-space:nowrap">Blue (A200)</span>    | #448AFF   | 68,138,255     | 218,73,100     |
| material | <p style="background-color: #2979FF">　　　</p>   | BLUE_A400                  | <span style="white-space:nowrap">Blue (A400)</span>    | #2979FF   | 41,121,255     | 218,84,100     |
| material | <p style="background-color: #2962FF">　　　</p>   | BLUE_A700                  | <span style="white-space:nowrap">Blue (A700)</span>    | #2962FF   | 41,98,255      | 224,84,100     |
| material | <p style="background-color: #607D8B">　　　</p>   | BLUE_GREY                  | <span style="white-space:nowrap">Blue Grey (500)</span>    | #607D8B   | 96,125,139     | 200,31,55      |
| material | <p style="background-color: #ECEFF1">　　　</p>   | BLUE_GREY_50               | <span style="white-space:nowrap">Blue Grey (50)</span>     | #ECEFF1   | 236,239,241    | 204,2,95       |
| material | <p style="background-color: #CFD8DC">　　　</p>   | BLUE_GREY_100              | <span style="white-space:nowrap">Blue Grey (100)</span>    | #CFD8DC   | 207,216,220    | 198,6,86       |
| material | <p style="background-color: #B0BBC5">　　　</p>   | BLUE_GREY_200              | <span style="white-space:nowrap">Blue Grey (200)</span>    | #B0BBC5   | 176,187,197    | 209,11,77      |
| material | <p style="background-color: #90A4AE">　　　</p>   | BLUE_GREY_300              | <span style="white-space:nowrap">Blue Grey (300)</span>    | #90A4AE   | 144,164,174    | 200,17,68      |
| material | <p style="background-color: #78909C">　　　</p>   | BLUE_GREY_400              | <span style="white-space:nowrap">Blue Grey (400)</span>    | #78909C   | 120,144,156    | 200,23,61      |
| material | <p style="background-color: #607D8B">　　　</p>   | BLUE_GREY_500              | <span style="white-space:nowrap">Blue Grey (500)</span>    | #607D8B   | 96,125,139     | 200,31,55      |
| material | <p style="background-color: #546E7A">　　　</p>   | BLUE_GREY_600              | <span style="white-space:nowrap">Blue Grey (600)</span>    | #546E7A   | 84,110,122     | 199,31,48      |
| material | <p style="background-color: #455A64">　　　</p>   | BLUE_GREY_700              | <span style="white-space:nowrap">Blue Grey (700)</span>    | #455A64   | 69,90,100      | 199,31,39      |
| material | <p style="background-color: #37474F">　　　</p>   | BLUE_GREY_800              | <span style="white-space:nowrap">Blue Grey (800)</span>    | #37474F   | 55,71,79       | 200,30,31      |
| material | <p style="background-color: #263238">　　　</p>   | BLUE_GREY_900              | <span style="white-space:nowrap">Blue Grey (900)</span>    | #263238   | 38,50,56       | 200,32,22      |
| css      | <p style="background-color: #8A2BE2">　　　</p>   | BLUE_VIOLET                | <span style="white-space:nowrap">Blue Violet</span>          | #8A2BE2   | 138,43,226     | 271,81,89      |
| web      | <p style="background-color: #66FF00">　　　</p>   | BRIGHT_GREEN               | <span style="white-space:nowrap">Bright Green / Vivid Green</span>     | #66FF00   | 102,255,0      | 96,100,100     |
| web      | <p style="background-color: #CD7F32">　　　</p>   | BRONZE                     | <span style="white-space:nowrap">Bronze</span>           | #CD7F32   | 184,115,51     | 29,72,72       |
| css      | <p style="background-color: #A52A2A">　　　</p>   | BROWN                      | <span style="white-space:nowrap">Brown</span>           | #A52A2A   | 165,42,42      | 0,75,65        |
| material | <p style="background-color: #EFEBE9">　　　</p>   | BROWN_50                   | <span style="white-space:nowrap">Brown (50)</span>      | #EFEBE9   | 239,235,233    | 20,3,94        |
| material | <p style="background-color: #D7CCC8">　　　</p>   | BROWN_100                  | <span style="white-space:nowrap">Brown (100)</span>     | #D7CCC8   | 215,204,200    | 16,7,84        |
| material | <p style="background-color: #BCAAA4">　　　</p>   | BROWN_200                  | <span style="white-space:nowrap">Brown (200)</span>     | #BCAAA4   | 188,170,164    | 15,13,74       |
| material | <p style="background-color: #A1887F">　　　</p>   | BROWN_300                  | <span style="white-space:nowrap">Brown (300)</span>     | #A1887F   | 161,136,127    | 16,21,63       |
| material | <p style="background-color: #8D6E63">　　　</p>   | BROWN_400                  | <span style="white-space:nowrap">Brown (400)</span>     | #8D6E63   | 141,110,99     | 16,30,55       |
| material | <p style="background-color: #795548">　　　</p>   | BROWN_500                  | <span style="white-space:nowrap">Brown (500)</span>     | #795548   | 121,85,72      | 16,40,47       |
| material | <p style="background-color: #6D4C41">　　　</p>   | BROWN_600                  | <span style="white-space:nowrap">Brown (600)</span>     | #6D4C41   | 109,76,65      | 15,40,43       |
| material | <p style="background-color: #5D4037">　　　</p>   | BROWN_700                  | <span style="white-space:nowrap">Brown (700)</span>     | #5D4037   | 93,64,55       | 14,41,36       |
| material | <p style="background-color: #4E342E">　　　</p>   | BROWN_800                  | <span style="white-space:nowrap">Brown (800)</span>     | #4E342E   | 78,52,46       | 11,41,31       |
| material | <p style="background-color: #3E2723">　　　</p>   | BROWN_900                  | <span style="white-space:nowrap">Brown (900)</span>     | #3E2723   | 62,39,35       | 9,44,24        |
| web      | <p style="background-color: #800020">　　　</p>   | BURGUNDY                   | <span style="white-space:nowrap">Burgundy</span>       | #800020   | 128,0,32       | 345,100,50     |
| css      | <p style="background-color: #DEB887">　　　</p>   | BURLY_WOOD                 | <span style="white-space:nowrap">Burly Wood</span>          | #DEB887   | 222,184,135    | 34,39,87       |
| web      | <p style="background-color: #CC5500">　　　</p>   | BURNT_ORANGE               | <span style="white-space:nowrap">Burnt Orange</span>          | #CC5500   | 204,85,0       | 25,100,80      |
| css      | <p style="background-color: #5F9EA0">　　　</p>   | CADET_BLUE                 | <span style="white-space:nowrap">Cadet Blue</span>         | #5F9EA0   | 95,158,160     | 182,41,63      |
| web      | <p style="background-color: #A16B47">　　　</p>   | CAMEL                      | <span style="white-space:nowrap">Camel</span>           | #A16B47   | 161,107,71     | 24,56,63       |
| web      | <p style="background-color: #E63995">　　　</p>   | CAMELLIA                   | <span style="white-space:nowrap">Camellia</span>         | #E63995   | 230,57,149     | 328,75,90      |
| web      | <p style="background-color: #FFEF00">　　　</p>   | CANARY_YELLOW              | <span style="white-space:nowrap">Canary Yellow</span>          | #FFEF00   | 255,239,0      | 56,100,100     |
| web      | <p style="background-color: #990036">　　　</p>   | CARDINAL_RED               | <span style="white-space:nowrap">Cardinal Red</span>         | #990036   | 153,0,54       | 339,100,60     |
| web      | <p style="background-color: #E6005C">　　　</p>   | CARMINE                    | <span style="white-space:nowrap">Carmine</span>         | #E6005C   | 230,0,92       | 336,100,90     |
| web      | <p style="background-color: #ACE1AF">　　　</p>   | CELADON                    | <span style="white-space:nowrap">Celadon</span>         | #ACE1AF   | 172,225,175    | 123,24,88      |
| web      | <p style="background-color: #DE3163">　　　</p>   | CERISE                     | <span style="white-space:nowrap">Cerise</span>    | #DE3163   | 222,49,99      | 343,78,87      |
| web      | <p style="background-color: #2A52BE">　　　</p>   | CERULEAN_BLUE              | <span style="white-space:nowrap">Cerulean Blue</span>    | #2A52BE   | 42,82,190      | 224,78,75      |
| web      | <p style="background-color: #FFFF99">　　　</p>   | CHAMPAGNE_YELLOW           | <span style="white-space:nowrap">Champagne Yellow</span>         | #FFFF99   | 255,255,153    | 60,40,100      |
| css      | <p style="background-color: #7FFF00">　　　</p>   | CHARTREUSE                 | <span style="white-space:nowrap">Chartreuse</span>        | #7FFF00   | 127,255,0      | 90,100,100     |
| css      | <p style="background-color: #D2691E">　　　</p>   | CHOCOLATE                  | <span style="white-space:nowrap">Chocolate</span>         | #D2691E   | 210,105,30     | 25,86,82       |
| web      | <p style="background-color: #E6B800">　　　</p>   | CHROME_YELLOW              | <span style="white-space:nowrap">Chrome Yellow</span>          | #E6B800   | 230,184,0      | 48,100,90      |
| web      | <p style="background-color: #CCA3CC">　　　</p>   | CLEMATIS                   | <span style="white-space:nowrap">Clematis</span>        | #CCA3CC   | 204,163,204    | 300,20,80      |
| web      | <p style="background-color: #0047AB">　　　</p>   | COBALT_BLUE                | <span style="white-space:nowrap">Cobalt Blue</span>          | #0047AB   | 0,71,171       | 215,100,67     |
| web      | <p style="background-color: #66FF59">　　　</p>   | COBALT_GREEN               | <span style="white-space:nowrap">Cobalt Green</span>          | #66FF59   | 102,255,89     | 115,65,100     |
| web      | <p style="background-color: #4D1F00">　　　</p>   | COCONUT_BROWN              | <span style="white-space:nowrap">Coconut Brown</span>          | #4D1F00   | 77,31,0        | 24,100,30      |
| web      | <p style="background-color: #4D3900">　　　</p>   | COFFEE                     | <span style="white-space:nowrap">Coffee</span>          | #4D3900   | 77,57,0        | 44,100,30      |
| css      | <p style="background-color: #FF7F50">　　　</p>   | CORAL                      | <span style="white-space:nowrap">Coral</span>         | #FF7F50   | 255,127,80     | 16,69,100      |
| web      | <p style="background-color: #FF80BF">　　　</p>   | CORAL_PINK                 | <span style="white-space:nowrap">Coral Pink</span>        | #FF80BF   | 255,128,191    | 330,50,100     |
| css      | <p style="background-color: #6495ED">　　　</p>   | CORNFLOWER_BLUE            | <span style="white-space:nowrap">Cornflower Blue</span>        | #6495ED   | 100,149,237    | 219,58,93      |
| css      | <p style="background-color: #FFF8DC">　　　</p>   | CORN_SILK                  | <span style="white-space:nowrap">Corn Silk</span>         | #FFF8DC   | 255,248,220    | 48,14,100      |
| web      | <p style="background-color: #FFFDD0">　　　</p>   | CREAM                      | <span style="white-space:nowrap">Cream</span>          | #FFFDD0   | 255,253,208    | 57,18,100      |
| css      | <p style="background-color: #DC143C">　　　</p>   | CRIMSON                    | <span style="white-space:nowrap">Crimson</span>          | #DC143C   | 220,20,60      | 348,91,86      |
| android  | <p style="background-color: #00FFFF">　　　</p>   | CYAN                       | <span style="white-space:nowrap">Cyan</span>           | #00FFFF   | 0,255,255      | 180,100,100    |
| material | <p style="background-color: #E0F7FA">　　　</p>   | CYAN_50                    | <span style="white-space:nowrap">Cyan (50)</span>      | #E0F7FA   | 224,247,250    | 187,10,98      |
| material | <p style="background-color: #B2EBF2">　　　</p>   | CYAN_100                   | <span style="white-space:nowrap">Cyan (100)</span>     | #B2EBF2   | 178,235,242    | 187,26,95      |
| material | <p style="background-color: #80DEEA">　　　</p>   | CYAN_200                   | <span style="white-space:nowrap">Cyan (200)</span>     | #80DEEA   | 128,222,234    | 187,45,92      |
| material | <p style="background-color: #4DD0E1">　　　</p>   | CYAN_300                   | <span style="white-space:nowrap">Cyan (300)</span>     | #4DD0E1   | 77,208,225     | 187,66,88      |
| material | <p style="background-color: #26C6DA">　　　</p>   | CYAN_400                   | <span style="white-space:nowrap">Cyan (400)</span>     | #26C6DA   | 38,198,218     | 187,83,85      |
| material | <p style="background-color: #00BCD4">　　　</p>   | CYAN_500                   | <span style="white-space:nowrap">Cyan (500)</span>     | #00BCD4   | 0,188,212      | 187,100,83     |
| material | <p style="background-color: #00ACC1">　　　</p>   | CYAN_600                   | <span style="white-space:nowrap">Cyan (600)</span>     | #00ACC1   | 0,172,193      | 187,100,76     |
| material | <p style="background-color: #0097A7">　　　</p>   | CYAN_700                   | <span style="white-space:nowrap">Cyan (700)</span>     | #0097A7   | 0,151,167      | 186,100,65     |
| material | <p style="background-color: #00838F">　　　</p>   | CYAN_800                   | <span style="white-space:nowrap">Cyan (800)</span>     | #00838F   | 0,131,143      | 185,100,56     |
| material | <p style="background-color: #006064">　　　</p>   | CYAN_900                   | <span style="white-space:nowrap">Cyan (900)</span>     | #006064   | 0,96,100       | 182,100,39     |
| material | <p style="background-color: #84FFFF">　　　</p>   | CYAN_A100                  | <span style="white-space:nowrap">Cyan (A100)</span>    | #84FFFF   | 132,255,255    | 180,48,100     |
| material | <p style="background-color: #18FFFF">　　　</p>   | CYAN_A200                  | <span style="white-space:nowrap">Cyan (A200)</span>    | #18FFFF   | 24,255,255     | 180,91,100     |
| material | <p style="background-color: #00E5FF">　　　</p>   | CYAN_A400                  | <span style="white-space:nowrap">Cyan (A400)</span>    | #00E5FF   | 0,229,255      | 186,100,100    |
| material | <p style="background-color: #00B8D4">　　　</p>   | CYAN_A700                  | <span style="white-space:nowrap">Cyan (A700)</span>    | #00B8D4   | 0,184,212      | 188,100,83     |
| web      | <p style="background-color: #0DBF8C">　　　</p>   | CYAN_BLUE                  | <span style="white-space:nowrap">Cyan Blue</span>          | #0DBF8C   | 13,191,140     | 163,93,75      |
| css      | <p style="background-color: #00008B">　　　</p>   | DARK_BLUE                  | <span style="white-space:nowrap">Dark Blue</span>          | #00008B   | 0,0,139        | 240,100,55     |
| css      | <p style="background-color: #008B8B">　　　</p>   | DARK_CYAN                  | <span style="white-space:nowrap">Dark Cyan</span>          | #008B8B   | 0,139,139      | 180,100,55     |
| css      | <p style="background-color: #B8860B">　　　</p>   | DARK_GOLDENROD             | <span style="white-space:nowrap">Dark Goldenrod</span>         | #B8860B   | 184,134,11     | 43,94,72       |
| android  | <p style="background-color: #444444">　　　</p>   | DARK_GRAY                  | <span style="white-space:nowrap">Dark Gray</span>          | #444444   | 68,68,68       | 0,0,27         |
| css      | <p style="background-color: #006400">　　　</p>   | DARK_GREEN                 | <span style="white-space:nowrap">Dark Green</span>          | #006400   | 0,100,0        | 120,100,39     |
| android  | <p style="background-color: #444444">　　　</p>   | DARK_GREY                  | <span style="white-space:nowrap">Dark Gray</span>          | #444444   | 68,68,68       | 0,0,27         |
| css      | <p style="background-color: #BDB76B">　　　</p>   | DARK_KHAKI                 | <span style="white-space:nowrap">Dark Khaki</span>         | #BDB76B   | 189,183,107    | 56,43,74       |
| css      | <p style="background-color: #8B008B">　　　</p>   | DARK_MAGENTA               | <span style="white-space:nowrap">Dark Magenta</span>         | #8B008B   | 139,0,139      | 300,100,55     |
| web      | <p style="background-color: #24367D">　　　</p>   | DARK_MINERAL_BLUE          | <span style="white-space:nowrap">Dark Mineral Blue</span>         | #24367D   | 36,54,125      | 228,71,49      |
| css      | <p style="background-color: #556B2F">　　　</p>   | DARK_OLIVE_GREEN           | <span style="white-space:nowrap">Dark Olive Green</span>        | #556B2F   | 85,107,47      | 82,56,42       |
| css      | <p style="background-color: #FF8C00">　　　</p>   | DARK_ORANGE                | <span style="white-space:nowrap">Dark Orange</span>          | #FF8C00   | 255,140,0      | 33,100,100     |
| css      | <p style="background-color: #9932CC">　　　</p>   | DARK_ORCHID                | <span style="white-space:nowrap">Dark Orchid</span>         | #9932CC   | 153,50,204     | 280,75,80      |
| web      | <p style="background-color: #003399">　　　</p>   | DARK_POWDER_BLUE           | <span style="white-space:nowrap">Dark Powder Blue</span>         | #003399   | 0,51,153       | 220,100,60     |
| css      | <p style="background-color: #8B0000">　　　</p>   | DARK_RED                   | <span style="white-space:nowrap">Dark Red</span>          | #8B0000   | 139,0,0        | 0,100,55       |
| css      | <p style="background-color: #E9967A">　　　</p>   | DARK_SALMON                | <span style="white-space:nowrap">Dark Salmon</span>         | #E9967A   | 233,150,122    | 15,48,91       |
| css      | <p style="background-color: #8FBC8F">　　　</p>   | DARK_SEA_GREEN             | <span style="white-space:nowrap">Dark Sea Green</span>         | #8FBC8F   | 143,188,143    | 120,24,74      |
| css      | <p style="background-color: #483D8B">　　　</p>   | DARK_SLATE_BLUE            | <span style="white-space:nowrap">Dark Slate Blue</span>         | #483D8B   | 72,61,139      | 248,56,55      |
| css      | <p style="background-color: #2F4F4F">　　　</p>   | DARK_SLATE_GRAY            | <span style="white-space:nowrap">Dark Slate Gray</span>         | #2F4F4F   | 47,79,79       | 180,41,31      |
| css      | <p style="background-color: #2F4F4F">　　　</p>   | DARK_SLATE_GREY            | <span style="white-space:nowrap">Dark Slate Gray</span>         | #2F4F4F   | 47,79,79       | 180,41,31      |
| css      | <p style="background-color: #00CED1">　　　</p>   | DARK_TURQUOISE             | <span style="white-space:nowrap">Dark Turquoise</span>        | #00CED1   | 0,206,209      | 181,100,82     |
| css      | <p style="background-color: #9400D3">　　　</p>   | DARK_VIOLET                | <span style="white-space:nowrap">Dark Violet</span>          | #9400D3   | 148,0,211      | 282,100,83     |
| material | <p style="background-color: #FF5722">　　　</p>   | DEEP_ORANGE                | <span style="white-space:nowrap">Deep Orange (500)</span>    | #FF5722   | 255,87,34      | 14,87,100      |
| material | <p style="background-color: #FBE9A7">　　　</p>   | DEEP_ORANGE_50             | <span style="white-space:nowrap">Deep Orange (50)</span>     | #FBE9A7   | 251,233,167    | 47,33,98       |
| material | <p style="background-color: #FFCCBC">　　　</p>   | DEEP_ORANGE_100            | <span style="white-space:nowrap">Deep Orange (100)</span>    | #FFCCBC   | 255,204,188    | 14,26,100      |
| material | <p style="background-color: #FFAB91">　　　</p>   | DEEP_ORANGE_200            | <span style="white-space:nowrap">Deep Orange (200)</span>    | #FFAB91   | 255,171,145    | 14,43,100      |
| material | <p style="background-color: #FF8A65">　　　</p>   | DEEP_ORANGE_300            | <span style="white-space:nowrap">Deep Orange (300)</span>    | #FF8A65   | 255,138,101    | 14,60,100      |
| material | <p style="background-color: #FF7043">　　　</p>   | DEEP_ORANGE_400            | <span style="white-space:nowrap">Deep Orange (400)</span>    | #FF7043   | 255,112,67     | 14,74,100      |
| material | <p style="background-color: #FF5722">　　　</p>   | DEEP_ORANGE_500            | <span style="white-space:nowrap">Deep Orange (500)</span>    | #FF5722   | 255,87,34      | 14,87,100      |
| material | <p style="background-color: #F4511E">　　　</p>   | DEEP_ORANGE_600            | <span style="white-space:nowrap">Deep Orange (600)</span>    | #F4511E   | 244,81,30      | 14,88,96       |
| material | <p style="background-color: #E64A19">　　　</p>   | DEEP_ORANGE_700            | <span style="white-space:nowrap">Deep Orange (700)</span>    | #E64A19   | 230,74,25      | 14,89,90       |
| material | <p style="background-color: #D84315">　　　</p>   | DEEP_ORANGE_800            | <span style="white-space:nowrap">Deep Orange (800)</span>    | #D84315   | 216,67,21      | 14,90,85       |
| material | <p style="background-color: #BF360C">　　　</p>   | DEEP_ORANGE_900            | <span style="white-space:nowrap">Deep Orange (900)</span>    | #BF360C   | 191,54,12      | 14,94,75       |
| material | <p style="background-color: #FF9E80">　　　</p>   | DEEP_ORANGE_A100           | <span style="white-space:nowrap">Deep Orange (A100)</span>   | #FF9E80   | 255,158,128    | 14,50,100      |
| material | <p style="background-color: #FF6E40">　　　</p>   | DEEP_ORANGE_A200           | <span style="white-space:nowrap">Deep Orange (A200)</span>   | #FF6E40   | 255,110,64     | 14,75,100      |
| material | <p style="background-color: #FF3D00">　　　</p>   | DEEP_ORANGE_A400           | <span style="white-space:nowrap">Deep Orange (A400)</span>   | #FF3D00   | 255,61,0       | 14,100,100     |
| material | <p style="background-color: #DD2600">　　　</p>   | DEEP_ORANGE_A700           | <span style="white-space:nowrap">Deep Orange (A700)</span>   | #DD2600   | 221,38,0       | 10,100,87      |
| css      | <p style="background-color: #FF1493">　　　</p>   | DEEP_PINK                  | <span style="white-space:nowrap">Deep Pink</span>         | #FF1493   | 255,20,147     | 328,92,100     |
| material | <p style="background-color: #673AB7">　　　</p>   | DEEP_PURPLE                | <span style="white-space:nowrap">Deep Purple (500)</span>    | #673AB7   | 103,58,183     | 262,68,72      |
| material | <p style="background-color: #EDE7F6">　　　</p>   | DEEP_PURPLE_50             | <span style="white-space:nowrap">Deep Purple (50)</span>     | #EDE7F6   | 237,231,246    | 264,6,96       |
| material | <p style="background-color: #D1C4E9">　　　</p>   | DEEP_PURPLE_100            | <span style="white-space:nowrap">Deep Purple (100)</span>    | #D1C4E9   | 209,196,233    | 261,16,91      |
| material | <p style="background-color: #B39DDB">　　　</p>   | DEEP_PURPLE_200            | <span style="white-space:nowrap">Deep Purple (200)</span>    | #B39DDB   | 179,157,219    | 261,28,86      |
| material | <p style="background-color: #9575CD">　　　</p>   | DEEP_PURPLE_300            | <span style="white-space:nowrap">Deep Purple (300)</span>    | #9575CD   | 149,117,205    | 262,43,80      |
| material | <p style="background-color: #7E57C2">　　　</p>   | DEEP_PURPLE_400            | <span style="white-space:nowrap">Deep Purple (400)</span>    | #7E57C2   | 126,87,194     | 262,55,76      |
| material | <p style="background-color: #673AB7">　　　</p>   | DEEP_PURPLE_500            | <span style="white-space:nowrap">Deep Purple (500)</span>    | #673AB7   | 103,58,183     | 262,68,72      |
| material | <p style="background-color: #5E35B1">　　　</p>   | DEEP_PURPLE_600            | <span style="white-space:nowrap">Deep Purple (600)</span>    | #5E35B1   | 94,53,177      | 260,70,69      |
| material | <p style="background-color: #512DA8">　　　</p>   | DEEP_PURPLE_700            | <span style="white-space:nowrap">Deep Purple (700)</span>    | #512DA8   | 81,45,168      | 258,73,66      |
| material | <p style="background-color: #4527A0">　　　</p>   | DEEP_PURPLE_800            | <span style="white-space:nowrap">Deep Purple (800)</span>    | #4527A0   | 69,39,160      | 255,76,63      |
| material | <p style="background-color: #311B92">　　　</p>   | DEEP_PURPLE_900            | <span style="white-space:nowrap">Deep Purple (900)</span>    | #311B92   | 49,27,146      | 251,82,57      |
| material | <p style="background-color: #B388FF">　　　</p>   | DEEP_PURPLE_A100           | <span style="white-space:nowrap">Deep Purple (A100)</span>   | #B388FF   | 179,136,255    | 262,47,100     |
| material | <p style="background-color: #7C4DFF">　　　</p>   | DEEP_PURPLE_A200           | <span style="white-space:nowrap">Deep Purple (A200)</span>   | #7C4DFF   | 124,77,255     | 256,70,100     |
| material | <p style="background-color: #651FFF">　　　</p>   | DEEP_PURPLE_A400           | <span style="white-space:nowrap">Deep Purple (A400)</span>   | #651FFF   | 101,31,255     | 259,88,100     |
| material | <p style="background-color: #6200EA">　　　</p>   | DEEP_PURPLE_A700           | <span style="white-space:nowrap">Deep Purple (A700)</span>   | #6200EA   | 98,0,234       | 265,100,92     |
| css      | <p style="background-color: #00BFFF">　　　</p>   | DEEP_SKY_BLUE              | <span style="white-space:nowrap">Deep Sky Blue</span>         | #00BFFF   | 0,191,255      | 195,100,100    |
| css      | <p style="background-color: #696969">　　　</p>   | DIM_GRAY                   | <span style="white-space:nowrap">Dim Gray</span>          | #696969   | 105,105,105    | 0,0,41         |
| css      | <p style="background-color: #696969">　　　</p>   | DIM_GREY                   | <span style="white-space:nowrap">Dim Gray</span>          | #696969   | 105,105,105    | 0,0,41         |
| android  | <p style="background-color: #444444">　　　</p>   | DKGRAY                     | <span style="white-space:nowrap">Dark Gray</span>          | #444444   | 68,68,68       | 0,0,27         |
| css      | <p style="background-color: #1E90FF">　　　</p>   | DODGER_BLUE                | <span style="white-space:nowrap">Dodger Blue</span>         | #1E90FF   | 30,144,255     | 210,88,100     |
| web      | <p style="background-color: #50C878">　　　</p>   | EMERALD                    | <span style="white-space:nowrap">Emerald</span>          | #50C878   | 80,200,120     | 140,60,78      |
| css      | <p style="background-color: #B22222">　　　</p>   | FIRE_BRICK                 | <span style="white-space:nowrap">Fire Brick</span>          | #B22222   | 178,34,34      | 0,81,70        |
| web      | <p style="background-color: #E68AB8">　　　</p>   | FLAMINGO                   | <span style="white-space:nowrap">Flamingo</span>         | #E68AB8   | 230,138,184    | 330,40,90      |
| css      | <p style="background-color: #FFFAF0">　　　</p>   | FLORAL_WHITE               | <span style="white-space:nowrap">Floral White</span>         | #FFFAF0   | 255,250,240    | 40,6,100       |
| web      | <p style="background-color: #73B839">　　　</p>   | FOLIAGE_GREEN              | <span style="white-space:nowrap">Foliage Green</span>          | #73B839   | 115,184,57     | 93,69,72       |
| css      | <p style="background-color: #228B22">　　　</p>   | FOREST_GREEN               | <span style="white-space:nowrap">Forest Green</span>         | #228B22   | 34,139,34      | 120,76,55      |
| web      | <p style="background-color: #99FF4D">　　　</p>   | FRESH_LEAVES               | <span style="white-space:nowrap">Fresh Green</span>          | #99FF4D   | 153,255,77     | 94,70,100      |
| android  | <p style="background-color: #FF00FF">　　　</p>   | FUCHSIA                    | <span style="white-space:nowrap">Magenta / Fuchsia</span>     | #FF00FF   | 255,0,255      | 300,100,100    |
| css      | <p style="background-color: #DCDCDC">　　　</p>   | GAINSBORO                  | <span style="white-space:nowrap">Gainsboro Gray</span>       | #DCDCDC   | 220,220,220    | 0,0,86         |
| css      | <p style="background-color: #F8F8FF">　　　</p>   | GHOST_WHITE                | <span style="white-space:nowrap">Ghost White</span>         | #F8F8FF   | 248,248,255    | 240,3,100      |
| css      | <p style="background-color: #FFD700">　　　</p>   | GOLD                       | <span style="white-space:nowrap">Gold</span>           | #FFD700   | 255,215,0      | 51,100,100     |
| web      | <p style="background-color: #FFD700">　　　</p>   | GOLDEN                     | <span style="white-space:nowrap">Gold</span>           | #FFD700   | 255,215,0      | 51,100,100     |
| css      | <p style="background-color: #DAA520">　　　</p>   | GOLDENROD                  | <span style="white-space:nowrap">Goldenrod</span>          | #DAA520   | 218,165,32     | 43,85,85       |
| web      | <p style="background-color: #99E64D">　　　</p>   | GRASS_GREEN                | <span style="white-space:nowrap">Grass Green</span>          | #99E64D   | 153,230,77     | 90,67,90       |
| android  | <p style="background-color: #888888">　　　</p>   | GRAY                       | <span style="white-space:nowrap">Gray</span>           | #888888   | 136,136,136    | 0,0,53         |
| web      | <p style="background-color: #8674A1">　　　</p>   | GRAYISH_PURPLE             | <span style="white-space:nowrap">Grayish Purple</span>         | #8674A1   | 134,116,161    | 264,28,63      |
| android  | <p style="background-color: #00FF00">　　　</p>   | GREEN                      | <span style="white-space:nowrap">Green</span>           | #00FF00   | 0,255,0        | 120,100,100    |
| material | <p style="background-color: #E8F5E9">　　　</p>   | GREEN_50                   | <span style="white-space:nowrap">Green (50)</span>      | #E8F5E9   | 232,245,233    | 125,5,96       |
| material | <p style="background-color: #C8E6C9">　　　</p>   | GREEN_100                  | <span style="white-space:nowrap">Green (100)</span>     | #C8E6C9   | 200,230,201    | 122,13,90      |
| material | <p style="background-color: #A5D6A7">　　　</p>   | GREEN_200                  | <span style="white-space:nowrap">Green (200)</span>     | #A5D6A7   | 165,214,167    | 122,23,84      |
| material | <p style="background-color: #81C784">　　　</p>   | GREEN_300                  | <span style="white-space:nowrap">Green (300)</span>     | #81C784   | 129,199,132    | 123,35,78      |
| material | <p style="background-color: #66BB6A">　　　</p>   | GREEN_400                  | <span style="white-space:nowrap">Green (400)</span>     | #66BB6A   | 102,187,106    | 123,45,73      |
| material | <p style="background-color: #4CAF50">　　　</p>   | GREEN_500                  | <span style="white-space:nowrap">Green (500)</span>     | #4CAF50   | 76,175,80      | 122,57,69      |
| material | <p style="background-color: #43A047">　　　</p>   | GREEN_600                  | <span style="white-space:nowrap">Green (600)</span>     | #43A047   | 67,160,71      | 123,58,63      |
| material | <p style="background-color: #388E3C">　　　</p>   | GREEN_700                  | <span style="white-space:nowrap">Green (700)</span>     | #388E3C   | 56,142,60      | 123,61,56      |
| material | <p style="background-color: #2E7D32">　　　</p>   | GREEN_800                  | <span style="white-space:nowrap">Green (800)</span>     | #2E7D32   | 46,125,50      | 123,63,49      |
| material | <p style="background-color: #1B5E20">　　　</p>   | GREEN_900                  | <span style="white-space:nowrap">Green (900)</span>     | #1B5E20   | 27,94,32       | 124,71,37      |
| material | <p style="background-color: #B9F6CA">　　　</p>   | GREEN_A100                 | <span style="white-space:nowrap">Green (A100)</span>    | #B9F6CA   | 185,246,202    | 137,25,96      |
| material | <p style="background-color: #69F0AE">　　　</p>   | GREEN_A200                 | <span style="white-space:nowrap">Green (A200)</span>    | #69F0AE   | 105,240,174    | 151,56,94      |
| material | <p style="background-color: #00E676">　　　</p>   | GREEN_A400                 | <span style="white-space:nowrap">Green (A400)</span>    | #00E676   | 0,230,118      | 151,100,90     |
| material | <p style="background-color: #00C853">　　　</p>   | GREEN_A700                 | <span style="white-space:nowrap">Green (A700)</span>    | #00C853   | 0,200,83       | 145,100,78     |
| css      | <p style="background-color: #ADFF2F">　　　</p>   | GREEN_YELLOW               | <span style="white-space:nowrap">Green Yellow</span>          | #ADFF2F   | 173,255,47     | 84,82,100      |
| android  | <p style="background-color: #888888">　　　</p>   | GREY                       | <span style="white-space:nowrap">Gray</span>           | #888888   | 136,136,136    | 0,0,53         |
| material | <p style="background-color: #FAFAFA">　　　</p>   | GREY_50                    | <span style="white-space:nowrap">Grey (50)</span>      | #FAFAFA   | 250,250,250    | 0,0,98         |
| material | <p style="background-color: #F5F5F5">　　　</p>   | GREY_100                   | <span style="white-space:nowrap">Grey (100)</span>     | #F5F5F5   | 245,245,245    | 0,0,96         |
| material | <p style="background-color: #EEEEEE">　　　</p>   | GREY_200                   | <span style="white-space:nowrap">Grey (200)</span>     | #EEEEEE   | 238,238,238    | 0,0,93         |
| material | <p style="background-color: #E0E0E0">　　　</p>   | GREY_300                   | <span style="white-space:nowrap">Grey (300)</span>     | #E0E0E0   | 224,224,224    | 0,0,88         |
| material | <p style="background-color: #BDBDBD">　　　</p>   | GREY_400                   | <span style="white-space:nowrap">Grey (400)</span>     | #BDBDBD   | 189,189,189    | 0,0,74         |
| material | <p style="background-color: #9E9E9E">　　　</p>   | GREY_500                   | <span style="white-space:nowrap">Grey (500)</span>     | #9E9E9E   | 158,158,158    | 0,0,62         |
| material | <p style="background-color: #757575">　　　</p>   | GREY_600                   | <span style="white-space:nowrap">Grey (600)</span>     | #757575   | 117,117,117    | 0,0,46         |
| material | <p style="background-color: #616161">　　　</p>   | GREY_700                   | <span style="white-space:nowrap">Grey (700)</span>     | #616161   | 97,97,97       | 0,0,38         |
| material | <p style="background-color: #424242">　　　</p>   | GREY_800                   | <span style="white-space:nowrap">Grey (800)</span>     | #424242   | 66,66,66       | 0,0,26         |
| material | <p style="background-color: #212121">　　　</p>   | GREY_900                   | <span style="white-space:nowrap">Grey (900)</span>     | #212121   | 33,33,33       | 0,0,13         |
| web      | <p style="background-color: #DF73FF">　　　</p>   | HELIOTROPE                 | <span style="white-space:nowrap">Heliotrope</span>         | #DF73FF   | 223,115,255    | 286,55,100     |
| css      | <p style="background-color: #F0FFF0">　　　</p>   | HONEYDEW                   | <span style="white-space:nowrap">Honeydew</span>         | #F0FFF0   | 240,255,240    | 120,6,100      |
| web      | <p style="background-color: #FFB366">　　　</p>   | HONEY_ORANGE               | <span style="white-space:nowrap">Honey Orange</span>          | #FFB366   | 255,179,102    | 30,60,100      |
| web      | <p style="background-color: #B8DDC8">　　　</p>   | HORIZON_BLUE               | <span style="white-space:nowrap">Horizon Blue</span>           | #B8DDC8   | 184,221,200    | 146,35,100     |
| css      | <p style="background-color: #FF69B4">　　　</p>   | HOT_PINK                   | <span style="white-space:nowrap">Hot Pink</span>         | #FF69B4   | 255,105,180    | 330,59,100     |
| css      | <p style="background-color: #CD5C5C">　　　</p>   | INDIAN_RED                 | <span style="white-space:nowrap">Indian Red</span>         | #CD5C5C   | 205,92,92      | 0,55,80        |
| css      | <p style="background-color: #4B0082">　　　</p>   | INDIGO                     | <span style="white-space:nowrap">Indigo</span>           | #4B0082   | 75,0,130       | 	275,100,51    |
| material | <p style="background-color: #E8EAF6">　　　</p>   | INDIGO_50                  | <span style="white-space:nowrap">Indigo (50)</span>     | #E8EAF6   | 232,234,246    | 231,6,96       |
| material | <p style="background-color: #C5CAE9">　　　</p>   | INDIGO_100                 | <span style="white-space:nowrap">Indigo (100)</span>    | #C5CAE9   | 197,202,233    | 232,15,91      |
| material | <p style="background-color: #9FA8DA">　　　</p>   | INDIGO_200                 | <span style="white-space:nowrap">Indigo (200)</span>    | #9FA8DA   | 159,168,218    | 231,27,85      |
| material | <p style="background-color: #7986CB">　　　</p>   | INDIGO_300                 | <span style="white-space:nowrap">Indigo (300)</span>    | #7986CB   | 121,134,203    | 230,40,80      |
| material | <p style="background-color: #5C6BC0">　　　</p>   | INDIGO_400                 | <span style="white-space:nowrap">Indigo (400)</span>    | #5C6BC0   | 92,107,192     | 231,52,75      |
| material | <p style="background-color: #3F51B5">　　　</p>   | INDIGO_500                 | <span style="white-space:nowrap">Indigo (500)</span>    | #3F51B5   | 63,81,181      | 231,65,71      |
| material | <p style="background-color: #3949AB">　　　</p>   | INDIGO_600                 | <span style="white-space:nowrap">Indigo (600)</span>    | #3949AB   | 57,73,171      | 232,67,67      |
| material | <p style="background-color: #303F9F">　　　</p>   | INDIGO_700                 | <span style="white-space:nowrap">Indigo (700)</span>    | #303F9F   | 48,63,159      | 232,70,62      |
| material | <p style="background-color: #283593">　　　</p>   | INDIGO_800                 | <span style="white-space:nowrap">Indigo (800)</span>    | #283593   | 40,53,147      | 233,73,58      |
| material | <p style="background-color: #1A237E">　　　</p>   | INDIGO_900                 | <span style="white-space:nowrap">Indigo (900)</span>    | #1A237E   | 26,35,126      | 235,79,49      |
| material | <p style="background-color: #8C9EFF">　　　</p>   | INDIGO_A100                | <span style="white-space:nowrap">Indigo (A100)</span>   | #8C9EFF   | 140,158,255    | 231,45,100     |
| material | <p style="background-color: #536DFE">　　　</p>   | INDIGO_A200                | <span style="white-space:nowrap">Indigo (A200)</span>   | #536DFE   | 83,109,254     | 231,67,100     |
| material | <p style="background-color: #3D5AFE">　　　</p>   | INDIGO_A400                | <span style="white-space:nowrap">Indigo (A400)</span>   | #3D5AFE   | 61,90,254      | 231,76,100     |
| material | <p style="background-color: #304FFE">　　　</p>   | INDIGO_A700                | <span style="white-space:nowrap">Indigo (A700)</span>   | #304FFE   | 48,79,254      | 231,81,100     |
| web      | <p style="background-color: #002FA7">　　　</p>   | INTERNATIONAL_KLEIN_BLUE   | <span style="white-space:nowrap">International Klein Blue</span>       | #002FA7   | 0,47,167       | 223,100,65     |
| web      | <p style="background-color: #625B57">　　　</p>   | IRON_GRAY                  | <span style="white-space:nowrap">Iron Gray</span>          | #625B57   | 98,91,87       | 21,12,39       |
| css      | <p style="background-color: #FFFFF0">　　　</p>   | IVORY                      | <span style="white-space:nowrap">Ivory</span>          | #FFFFF0   | 255,255,240    | 60,6,100       |
| web      | <p style="background-color: #36BF36">　　　</p>   | IVY_GREEN                  | <span style="white-space:nowrap">Ivy Green</span>        | #36BF36   | 54,191,54      | 120,72,75      |
| web      | <p style="background-color: #E6C35C">　　　</p>   | JASMINE                    | <span style="white-space:nowrap">Jasmine</span>         | #E6C35C   | 230,195,92     | 45,60,90       |
| css      | <p style="background-color: #F0E68C">　　　</p>   | KHAKI                      | <span style="white-space:nowrap">Khaki</span>          | #F0E68C   | 240,230,140    | 54,42,94       |
| web      | <p style="background-color: #26619C">　　　</p>   | LAPIS_LAZULI               | <span style="white-space:nowrap">Lapis Lazuli</span>        | #26619C   | 38,97,156      | 210,76,61      |
| css      | <p style="background-color: #E6E6FA">　　　</p>   | LAVENDER                   | <span style="white-space:nowrap">Lavender</span>         | #E6E6FA   | 230,230,250    | 240,8,98       |
| web      | <p style="background-color: #CCCCFF">　　　</p>   | LAVENDER_BLUE              | <span style="white-space:nowrap">Lavender Blue / Periwinkle</span>  | #CCCCFF   | 204,204,255    | 240,20,100     |
| css      | <p style="background-color: #FFF0F5">　　　</p>   | LAVENDER_BLUSH             | <span style="white-space:nowrap">Lavender Blush</span>       | #FFF0F5   | 255,240,245    | 340,6,100      |
| web      | <p style="background-color: #EE82EE">　　　</p>   | LAVENDER_MAGENTA           | <span style="white-space:nowrap">Lavender Magenta</span>          | #EE82EE   | 238,130,238    | 300,45,93      |
| web      | <p style="background-color: #E6E6FA">　　　</p>   | LAVENDER_MIST              | <span style="white-space:nowrap">Lavender Mist</span>        | #E6E6FA   | 230,230,250    | 240,8,98       |
| css      | <p style="background-color: #7CFC00">　　　</p>   | LAWN_GREEN                 | <span style="white-space:nowrap">Lawn Green</span>         | #7CFC00   | 124,252,0      | 90,100,99      |
| css      | <p style="background-color: #FFFACD">　　　</p>   | LEMON_CHIFFON              | <span style="white-space:nowrap">Lemon Chiffon</span>         | #FFFACD   | 255,250,205    | 54,20,100      |
| css      | <p style="background-color: #ADD8E6">　　　</p>   | LIGHT_BLUE                 | <span style="white-space:nowrap">Light Blue</span>          | #ADD8E6   | 173,216,230    | 195,25,90      |
| material | <p style="background-color: #E1F5FE">　　　</p>   | LIGHT_BLUE_50              | <span style="white-space:nowrap">Light Blue (50)</span>     | #E1F5FE   | 225,245,254    | 199,11,100     |
| material | <p style="background-color: #B3E5FC">　　　</p>   | LIGHT_BLUE_100             | <span style="white-space:nowrap">Light Blue (100)</span>    | #B3E5FC   | 179,229,252    | 199,29,99      |
| material | <p style="background-color: #81D4FA">　　　</p>   | LIGHT_BLUE_200             | <span style="white-space:nowrap">Light Blue (200)</span>    | #81D4FA   | 129,212,250    | 199,48,98      |
| material | <p style="background-color: #4FC3F7">　　　</p>   | LIGHT_BLUE_300             | <span style="white-space:nowrap">Light Blue (300)</span>    | #4FC3F7   | 79,195,247     | 199,68,97      |
| material | <p style="background-color: #29B6FC">　　　</p>   | LIGHT_BLUE_400             | <span style="white-space:nowrap">Light Blue (400)</span>    | #29B6FC   | 41,182,252     | 200,84,99      |
| material | <p style="background-color: #03A9F4">　　　</p>   | LIGHT_BLUE_500             | <span style="white-space:nowrap">Light Blue (500)</span>    | #03A9F4   | 3,169,244      | 199,99,96      |
| material | <p style="background-color: #039BE5">　　　</p>   | LIGHT_BLUE_600             | <span style="white-space:nowrap">Light Blue (600)</span>    | #039BE5   | 3,155,229      | 200,99,90      |
| material | <p style="background-color: #0288D1">　　　</p>   | LIGHT_BLUE_700             | <span style="white-space:nowrap">Light Blue (700)</span>    | #0288D1   | 2,136,209      | 201,99,82      |
| material | <p style="background-color: #0277BD">　　　</p>   | LIGHT_BLUE_800             | <span style="white-space:nowrap">Light Blue (800)</span>    | #0277BD   | 2,119,189      | 202,99,74      |
| material | <p style="background-color: #01579B">　　　</p>   | LIGHT_BLUE_900             | <span style="white-space:nowrap">Light Blue (900)</span>    | #01579B   | 1,87,155       | 206,99,61      |
| material | <p style="background-color: #80D8FF">　　　</p>   | LIGHT_BLUE_A100            | <span style="white-space:nowrap">Light Blue (A100)</span>   | #80D8FF   | 128,216,255    | 198,50,100     |
| material | <p style="background-color: #40C4FF">　　　</p>   | LIGHT_BLUE_A200            | <span style="white-space:nowrap">Light Blue (A200)</span>   | #40C4FF   | 64,196,255     | 199,75,100     |
| material | <p style="background-color: #00B0FF">　　　</p>   | LIGHT_BLUE_A400            | <span style="white-space:nowrap">Light Blue (A400)</span>   | #00B0FF   | 0,176,255      | 199,100,100    |
| material | <p style="background-color: #0091EA">　　　</p>   | LIGHT_BLUE_A700            | <span style="white-space:nowrap">Light Blue (A700)</span>   | #0091EA   | 0,145,234      | 203,100,92     |
| css      | <p style="background-color: #F08080">　　　</p>   | LIGHT_CORAL                | <span style="white-space:nowrap">Light Coral</span>         | #F08080   | 240,128,128    | 0,47,94        |
| css      | <p style="background-color: #E0FFFF">　　　</p>   | LIGHT_CYAN                 | <span style="white-space:nowrap">Light Cyan</span>          | #E0FFFF   | 224,255,255    | 180,12,100     |
| css      | <p style="background-color: #FAFAD2">　　　</p>   | LIGHT_GOLDENROD_YELLOW     | <span style="white-space:nowrap">Light Goldenrod Yellow</span>        | #FAFAD2   | 250,250,210    | 60,16,98       |
| android  | <p style="background-color: #CCCCCC">　　　</p>   | LIGHT_GRAY                 | <span style="white-space:nowrap">Light Gray</span>          | #CCCCCC   | 204,204,204    | 0,0,80         |
| css      | <p style="background-color: #90EE90">　　　</p>   | LIGHT_GREEN                | <span style="white-space:nowrap">Light Green</span>          | #90EE90   | 144,238,144    | 120,39,93      |
| material | <p style="background-color: #F1F8E9">　　　</p>   | LIGHT_GREEN_50             | <span style="white-space:nowrap">Light Green (50)</span>     | #F1F8E9   | 241,248,233    | 88,6,97        |
| material | <p style="background-color: #DCEDC8">　　　</p>   | LIGHT_GREEN_100            | <span style="white-space:nowrap">Light Green (100)</span>    | #DCEDC8   | 220,237,200    | 88,16,93       |
| material | <p style="background-color: #C5E1A5">　　　</p>   | LIGHT_GREEN_200            | <span style="white-space:nowrap">Light Green (200)</span>    | #C5E1A5   | 197,225,165    | 88,27,88       |
| material | <p style="background-color: #AED581">　　　</p>   | LIGHT_GREEN_300            | <span style="white-space:nowrap">Light Green (300)</span>    | #AED581   | 174,213,129    | 88,39,84       |
| material | <p style="background-color: #9CCC65">　　　</p>   | LIGHT_GREEN_400            | <span style="white-space:nowrap">Light Green (400)</span>    | #9CCC65   | 156,204,101    | 88,50,80       |
| material | <p style="background-color: #8BC34A">　　　</p>   | LIGHT_GREEN_500            | <span style="white-space:nowrap">Light Green (500)</span>    | #8BC34A   | 139,195,74     | 88,62,76       |
| material | <p style="background-color: #7CB342">　　　</p>   | LIGHT_GREEN_600            | <span style="white-space:nowrap">Light Green (600)</span>    | #7CB342   | 124,179,66     | 89,63,70       |
| material | <p style="background-color: #689F38">　　　</p>   | LIGHT_GREEN_700            | <span style="white-space:nowrap">Light Green (700)</span>    | #689F38   | 104,159,56     | 92,65,62       |
| material | <p style="background-color: #558B2F">　　　</p>   | LIGHT_GREEN_800            | <span style="white-space:nowrap">Light Green (800)</span>    | #558B2F   | 85,139,47      | 95,66,55       |
| material | <p style="background-color: #33691E">　　　</p>   | LIGHT_GREEN_900            | <span style="white-space:nowrap">Light Green (900)</span>    | #33691E   | 51,105,30      | 103,71,41      |
| material | <p style="background-color: #CCFF90">　　　</p>   | LIGHT_GREEN_A100           | <span style="white-space:nowrap">Light Green (A100)</span>   | #CCFF90   | 204,255,144    | 88,44,100      |
| material | <p style="background-color: #B2FF59">　　　</p>   | LIGHT_GREEN_A200           | <span style="white-space:nowrap">Light Green (A200)</span>   | #B2FF59   | 178,255,89     | 88,65,100      |
| material | <p style="background-color: #76FF03">　　　</p>   | LIGHT_GREEN_A400           | <span style="white-space:nowrap">Light Green (A400)</span>   | #76FF03   | 118,255,3      | 93,99,100      |
| material | <p style="background-color: #64DD17">　　　</p>   | LIGHT_GREEN_A700           | <span style="white-space:nowrap">Light Green (A700)</span>   | #64DD17   | 100,221,23     | 97,90,87       |
| android  | <p style="background-color: #CCCCCC">　　　</p>   | LIGHT_GREY                 | <span style="white-space:nowrap">Light Gray</span>          | #CCCCCC   | 204,204,204    | 0,0,80         |
| web      | <p style="background-color: #F0E68C">　　　</p>   | LIGHT_KHAKI                | <span style="white-space:nowrap">Light Khaki</span>         | #F0E68C   | 240,230,140    | 54,42,94       |
| web      | <p style="background-color: #CCFF00">　　　</p>   | LIGHT_LIME                 | <span style="white-space:nowrap">Lime / Light Lime</span>  | #CCFF00   | 204,255,0      | 72,100,100     |
| css      | <p style="background-color: #FFB6C1">　　　</p>   | LIGHT_PINK                 | <span style="white-space:nowrap">Light Pink</span>         | #FFB6C1   | 255,182,193    | 351,29,100     |
| css      | <p style="background-color: #FFA07A">　　　</p>   | LIGHT_SALMON               | <span style="white-space:nowrap">Light Salmon</span>         | #FFA07A   | 255,160,122    | 17,52,100      |
| css      | <p style="background-color: #20B2AA">　　　</p>   | LIGHT_SEA_GREEN            | <span style="white-space:nowrap">Light Sea Green</span>         | #20B2AA   | 32,178,170     | 177,82,70      |
| css      | <p style="background-color: #87CEFA">　　　</p>   | LIGHT_SKY_BLUE             | <span style="white-space:nowrap">Light Sky Blue</span>         | #87CEFA   | 135,206,250    | 203,46,98      |
| css      | <p style="background-color: #778899">　　　</p>   | LIGHT_SLATE_GRAY           | <span style="white-space:nowrap">Light Slate Gray</span>         | #778899   | 119,136,153    | 210,22,60      |
| css      | <p style="background-color: #778899">　　　</p>   | LIGHT_SLATE_GREY           | <span style="white-space:nowrap">Light Slate Gray</span>         | #778899   | 119,136,153    | 210,22,60      |
| css      | <p style="background-color: #B0C4DE">　　　</p>   | LIGHT_STEEL_BLUE           | <span style="white-space:nowrap">Light Steel Blue</span>         | #B0C4DE   | 176,196,222    | 214,21,87      |
| web      | <p style="background-color: #B09DB9">　　　</p>   | LIGHT_VIOLET               | <span style="white-space:nowrap">Lavender Magenta</span>          | #B09DB9   | 176,157,185    | 281,15,73      |
| css      | <p style="background-color: #FFFFE0">　　　</p>   | LIGHT_YELLOW               | <span style="white-space:nowrap">Light Yellow</span>          | #FFFFE0   | 255,255,224    | 60,12,100      |
| web      | <p style="background-color: #C8A2C8">　　　</p>   | LILAC                      | <span style="white-space:nowrap">Lilac</span>         | #C8A2C8   | 200,162,200    | 300,19,78      |
| android  | <p style="background-color: #00FF00">　　　</p>   | LIME                       | <span style="white-space:nowrap">Green</span>           | #00FF00   | 0,255,0        | 120,100,100    |
| material | <p style="background-color: #F9FBE7">　　　</p>   | LIME_50                    | <span style="white-space:nowrap">Lime (50)</span>     | #F9FBE7   | 249,251,231    | 66,8,98        |
| material | <p style="background-color: #F0F4C3">　　　</p>   | LIME_100                   | <span style="white-space:nowrap">Lime (100)</span>    | #F0F4C3   | 240,244,195    | 65,20,96       |
| material | <p style="background-color: #E6EE9C">　　　</p>   | LIME_200                   | <span style="white-space:nowrap">Lime (200)</span>    | #E6EE9C   | 230,238,156    | 66,34,93       |
| material | <p style="background-color: #DCE775">　　　</p>   | LIME_300                   | <span style="white-space:nowrap">Lime (300)</span>    | #DCE775   | 220,231,117    | 66,49,91       |
| material | <p style="background-color: #D4E157">　　　</p>   | LIME_400                   | <span style="white-space:nowrap">Lime (400)</span>    | #D4E157   | 212,225,87     | 66,61,88       |
| material | <p style="background-color: #CDDC39">　　　</p>   | LIME_500                   | <span style="white-space:nowrap">Lime (500)</span>    | #CDDC39   | 205,220,57     | 66,74,86       |
| material | <p style="background-color: #C0CA33">　　　</p>   | LIME_600                   | <span style="white-space:nowrap">Lime (600)</span>    | #C0CA33   | 192,202,51     | 64,75,79       |
| material | <p style="background-color: #A4B42B">　　　</p>   | LIME_700                   | <span style="white-space:nowrap">Lime (700)</span>    | #A4B42B   | 164,180,43     | 67,76,71       |
| material | <p style="background-color: #9E9D24">　　　</p>   | LIME_800                   | <span style="white-space:nowrap">Lime (800)</span>    | #9E9D24   | 158,157,36     | 60,77,62       |
| material | <p style="background-color: #827717">　　　</p>   | LIME_900                   | <span style="white-space:nowrap">Lime (900)</span>    | #827717   | 130,119,23     | 54,82,51       |
| material | <p style="background-color: #F4FF81">　　　</p>   | LIME_A100                  | <span style="white-space:nowrap">Lime (A100)</span>   | #F4FF81   | 244,255,129    | 65,49,100      |
| material | <p style="background-color: #EEFF41">　　　</p>   | LIME_A200                  | <span style="white-space:nowrap">Lime (A200)</span>   | #EEFF41   | 238,255,65     | 65,75,100      |
| material | <p style="background-color: #C6FF00">　　　</p>   | LIME_A400                  | <span style="white-space:nowrap">Lime (A400)</span>   | #C6FF00   | 198,255,0      | 73,100,100     |
| material | <p style="background-color: #AEEA00">　　　</p>   | LIME_A700                  | <span style="white-space:nowrap">Lime (A700)</span>   | #AEEA00   | 174,234,0      | 75,100,92      |
| css      | <p style="background-color: #32CD32">　　　</p>   | LIME_GREEN                 | <span style="white-space:nowrap">Lime Green</span>         | #32CD32   | 50,205,50      | 120,76,80      |
| css      | <p style="background-color: #FAF0E6">　　　</p>   | LINEN                      | <span style="white-space:nowrap">Linen</span>          | #FAF0E6   | 250,240,230    | 30,8,98        |
| android  | <p style="background-color: #CCCCCC">　　　</p>   | LTGRAY                     | <span style="white-space:nowrap">Light Gray</span>          | #CCCCCC   | 204,204,204    | 0,0,80         |
| android  | <p style="background-color: #FF00FF">　　　</p>   | MAGENTA                    | <span style="white-space:nowrap">Magenta / Fuchsia</span>     | #FF00FF   | 255,0,255      | 300,100,100    |
| web      | <p style="background-color: #FF0DA6">　　　</p>   | MAGENTA_ROSE               | <span style="white-space:nowrap">Magenta Rose</span>        | #FF0DA6   | 255,13,166     | 322,95,100     |
| web      | <p style="background-color: #22C32E">　　　</p>   | MALACHITE                  | <span style="white-space:nowrap">Malachite</span>        | #22C32E   | 34,195,46      | 124,83,76      |
| web      | <p style="background-color: #D94DFF">　　　</p>   | MALLOW                     | <span style="white-space:nowrap">Mallow</span>         | #D94DFF   | 217,77,255     | 287,70,100     |
| web      | <p style="background-color: #FF9900">　　　</p>   | MARIGOLD                   | <span style="white-space:nowrap">Marigold</span>        | #FF9900   | 255,153,0      | 36,100,100     |
| web      | <p style="background-color: #00477D">　　　</p>   | MARINE_BLUE                | <span style="white-space:nowrap">Marine Blue</span>         | #00477D   | 0,71,125       | 206,100,49     |
| android  | <p style="background-color: #800000">　　　</p>   | MAROON                     | <span style="white-space:nowrap">Maroon</span>           | #800000   | 128,0,0        | 0,100,50       |
| web      | <p style="background-color: #E0B0FF">　　　</p>   | MAUVE                      | <span style="white-space:nowrap">Mauve</span>         | #E0B0FF   | 224,176,255    | 276,31,100     |
| css      | <p style="background-color: #66CDAA">　　　</p>   | MEDIUM_AQUAMARINE          | <span style="white-space:nowrap">Medium Aquamarine</span>         | #66CDAA   | 102,205,170    | 160,50,80      |
| css      | <p style="background-color: #0000CD">　　　</p>   | MEDIUM_BLUE                | <span style="white-space:nowrap">Medium Blue</span>          | #0000CD   | 0,0,205        | 240,100,80     |
| css      | <p style="background-color: #DDA0DD">　　　</p>   | MEDIUM_LAVENDER_MAGENTA    | <span style="white-space:nowrap">Medium Lavender Magenta</span>          | #DDA0DD   | 221,160,221    | 300,28,87      |
| css      | <p style="background-color: #BA55D3">　　　</p>   | MEDIUM_ORCHID              | <span style="white-space:nowrap">Medium Orchid</span>         | #BA55D3   | 186,85,211     | 288,60,83      |
| css      | <p style="background-color: #9370DB">　　　</p>   | MEDIUM_PURPLE              | <span style="white-space:nowrap">Medium Purple</span>          | #9370DB   | 147,112,219    | 260,49,86      |
| css      | <p style="background-color: #3CB371">　　　</p>   | MEDIUM_SEA_GREEN           | <span style="white-space:nowrap">Medium Sea Green</span>         | #3CB371   | 60,179,113     | 147,66,70      |
| css      | <p style="background-color: #7B68EE">　　　</p>   | MEDIUM_SLATE_BLUE          | <span style="white-space:nowrap">Medium Slate Blue</span>         | #7B68EE   | 123,104,238    | 249,56,93      |
| css      | <p style="background-color: #00FA9A">　　　</p>   | MEDIUM_SPRING_GREEN        | <span style="white-space:nowrap">Medium Spring Green</span>         | #00FA9A   | 0,250,154      | 157,100,98     |
| css      | <p style="background-color: #48D1CC">　　　</p>   | MEDIUM_TURQUOISE           | <span style="white-space:nowrap">Medium Turquoise</span>        | #48D1CC   | 72,209,204     | 178,66,82      |
| css      | <p style="background-color: #C71585">　　　</p>   | MEDIUM_VIOLET_RED          | <span style="white-space:nowrap">Medium Violet Red</span>        | #C71585   | 199,21,133     | 322,89,78      |
| css      | <p style="background-color: #191970">　　　</p>   | MIDNIGHT_BLUE              | <span style="white-space:nowrap">Midnight Blue</span>         | #191970   | 25,25,112      | 240,78,44      |
| web      | <p style="background-color: #E6D933">　　　</p>   | MIMOSA                     | <span style="white-space:nowrap">Mimosa Yellow</span>        | #E6D933   | 230,217,51     | 56,78,90       |
| web      | <p style="background-color: #004D99">　　　</p>   | MINERAL_BLUE               | <span style="white-space:nowrap">Mineral Blue</span>          | #004D99   | 0,77,153       | 210,100,60     |
| web      | <p style="background-color: #A39DAE">　　　</p>   | MINERAL_VIOLET             | <span style="white-space:nowrap">Mineral Violet</span>          | #A39DAE   | 163,157,174    | 261,10,68      |
| web      | <p style="background-color: #16982B">　　　</p>   | MINT                       | <span style="white-space:nowrap">Mint Green</span>         | #16982B   | 22,152,43      | 130,86,60      |
| css      | <p style="background-color: #F5FFFA">　　　</p>   | MINT_CREAM                 | <span style="white-space:nowrap">Mint Cream</span>        | #F5FFFA   | 245,255,250    | 150,4,100      |
| css      | <p style="background-color: #FFE4E1">　　　</p>   | MISTY_ROSE                 | <span style="white-space:nowrap">Misty Rose</span>         | #FFE4E1   | 255,228,225    | 6,12,100       |
| css      | <p style="background-color: #FFE4B5">　　　</p>   | MOCCASIN                   | <span style="white-space:nowrap">Moccasin</span>         | #FFE4B5   | 255,228,181    | 38,29,100      |
| web      | <p style="background-color: #FFFF4D">　　　</p>   | MOON_YELLOW                | <span style="white-space:nowrap">Moon Yellow</span>          | #FFFF4D   | 255,255,77     | 60,70,100      |
| web      | <p style="background-color: #697723">　　　</p>   | MOSS_GREEN                 | <span style="white-space:nowrap">Moss Green</span>         | #697723   | 105,119,35     | 70,71,47       |
| web      | <p style="background-color: #CCCC4D">　　　</p>   | MUSTARD                    | <span style="white-space:nowrap">Mustard</span>         | #CCCC4D   | 204,204,77     | 60,62,80       |
| css      | <p style="background-color: #FFDEAD">　　　</p>   | NAVAJO_WHITE               | <span style="white-space:nowrap">Navajo White</span>        | #FFDEAD   | 255,222,173    | 36,32,100      |
| android  | <p style="background-color: #000080">　　　</p>   | NAVY                       | <span style="white-space:nowrap">Navy / Navy Blue</span>    | #000080   | 0,0,128        | 240,100,50     |
| web      | <p style="background-color: #000080">　　　</p>   | NAVY_BLUE                  | <span style="white-space:nowrap">Navy / Navy Blue</span>    | #000080   | 0,0,128        | 240,100,50     |
| web      | <p style="background-color: #CC7722">　　　</p>   | OCHER                      | <span style="white-space:nowrap">Ocher</span>           | #CC7722   | 204,119,34     | 30,83,80       |
| css      | <p style="background-color: #FDF5E6">　　　</p>   | OLD_LACE                   | <span style="white-space:nowrap">Old Lace</span>         | #FDF5E6   | 253,245,230    | 39,9,99        |
| web      | <p style="background-color: #C08081">　　　</p>   | OLD_ROSE                   | <span style="white-space:nowrap">Old Rose</span>         | #C08081   | 192,128,129    | 359,33,75      |
| android  | <p style="background-color: #808000">　　　</p>   | OLIVE                      | <span style="white-space:nowrap">Olive</span>          | #808000   | 128,128,0      | 60,100,50      |
| css      | <p style="background-color: #6B8E23">　　　</p>   | OLIVE_DRAB                 | <span style="white-space:nowrap">Olive Drab</span>       | #6B8E23   | 107,142,35     | 80,75,56       |
| web      | <p style="background-color: #B784A7">　　　</p>   | OPERA_MAUVE                | <span style="white-space:nowrap">Opera Mauve</span>        | #B784A7   | 183,132,167    | 319,28,72      |
| css      | <p style="background-color: #FFA500">　　　</p>   | ORANGE                     | <span style="white-space:nowrap">Orange</span>           | #FFA500   | 255,165,0      | 39,100,100     |
| material | <p style="background-color: #FFF3E0">　　　</p>   | ORANGE_50                  | <span style="white-space:nowrap">Orange (50)</span>      | #FFF3E0   | 255,243,224    | 37,12,100      |
| material | <p style="background-color: #FFE0B2">　　　</p>   | ORANGE_100                 | <span style="white-space:nowrap">Orange (100)</span>     | #FFE0B2   | 255,224,178    | 36,30,100      |
| material | <p style="background-color: #FFCC80">　　　</p>   | ORANGE_200                 | <span style="white-space:nowrap">Orange (200)</span>     | #FFCC80   | 255,204,128    | 36,50,100      |
| material | <p style="background-color: #FFB74D">　　　</p>   | ORANGE_300                 | <span style="white-space:nowrap">Orange (300)</span>     | #FFB74D   | 255,183,77     | 36,70,100      |
| material | <p style="background-color: #FFA726">　　　</p>   | ORANGE_400                 | <span style="white-space:nowrap">Orange (400)</span>     | #FFA726   | 255,167,38     | 36,85,100      |
| material | <p style="background-color: #FF9800">　　　</p>   | ORANGE_500                 | <span style="white-space:nowrap">Orange (500)</span>     | #FF9800   | 255,152,0      | 36,100,100     |
| material | <p style="background-color: #FB8C00">　　　</p>   | ORANGE_600                 | <span style="white-space:nowrap">Orange (600)</span>     | #FB8C00   | 251,140,0      | 33,100,98      |
| material | <p style="background-color: #F57C00">　　　</p>   | ORANGE_700                 | <span style="white-space:nowrap">Orange (700)</span>     | #F57C00   | 245,124,0      | 30,100,96      |
| material | <p style="background-color: #EF6C00">　　　</p>   | ORANGE_800                 | <span style="white-space:nowrap">Orange (800)</span>     | #EF6C00   | 239,108,0      | 27,100,94      |
| material | <p style="background-color: #E65100">　　　</p>   | ORANGE_900                 | <span style="white-space:nowrap">Orange (900)</span>     | #E65100   | 230,81,0       | 21,100,90      |
| material | <p style="background-color: #FFD180">　　　</p>   | ORANGE_A100                | <span style="white-space:nowrap">Orange (A100)</span>    | #FFD180   | 255,209,128    | 38,50,100      |
| material | <p style="background-color: #FFAB40">　　　</p>   | ORANGE_A200                | <span style="white-space:nowrap">Orange (A200)</span>    | #FFAB40   | 255,171,64     | 34,75,100      |
| material | <p style="background-color: #FF9100">　　　</p>   | ORANGE_A400                | <span style="white-space:nowrap">Orange (A400)</span>    | #FF9100   | 255,145,0      | 34,100,100     |
| material | <p style="background-color: #FF6D00">　　　</p>   | ORANGE_A700                | <span style="white-space:nowrap">Orange (A700)</span>    | #FF6D00   | 255,109,0      | 26,100,100     |
| css      | <p style="background-color: #FF4500">　　　</p>   | ORANGE_RED                 | <span style="white-space:nowrap">Orange Red</span>          | #FF4500   | 255,69,0       | 16,100,100     |
| css      | <p style="background-color: #DA70D6">　　　</p>   | ORCHID                     | <span style="white-space:nowrap">Orchid</span>     | #DA70D6   | 218,112,214    | 302,49,85      |
| web      | <p style="background-color: #E6CFE6">　　　</p>   | PAIL_LILAC                 | <span style="white-space:nowrap">Pail Lilac</span>        | #E6CFE6   | 230,207,230    | 300,10,90      |
| web      | <p style="background-color: #D1EDF2">　　　</p>   | PALE_BLUE                  | <span style="white-space:nowrap">Pale Blue</span>          | #D1EDF2   | 209,237,242    | 189,14,95      |
| web      | <p style="background-color: #5E86C1">　　　</p>   | PALE_DENIM                 | <span style="white-space:nowrap">Pale Denim</span> | #5E86C1   | 94,134,193     | 216,51,76      |
| css      | <p style="background-color: #EEE8AA">　　　</p>   | PALE_GOLDENROD             | <span style="white-space:nowrap">Pale Goldenrod</span>         | #EEE8AA   | 238,232,170    | 55,29,93       |
| css      | <p style="background-color: #98FB98">　　　</p>   | PALE_GREEN                 | <span style="white-space:nowrap">Pale Green</span>          | #98FB98   | 152,251,152    | 120,39,98      |
| web      | <p style="background-color: #CCB38C">　　　</p>   | PALE_OCHRE                 | <span style="white-space:nowrap">Pale Ochre</span>          | #CCB38C   | 204,179,140    | 37,31,80       |
| css      | <p style="background-color: #AFEEEE">　　　</p>   | PALE_TURQUOISE             | <span style="white-space:nowrap">Pale Turquoise</span>        | #AFEEEE   | 175,238,238    | 180,26,93      |
| css      | <p style="background-color: #DB7093">　　　</p>   | PALE_VIOLET_RED            | <span style="white-space:nowrap">Pale Violet Red</span>         | #DB7093   | 219,112,147    | 340,49,86      |
| web      | <p style="background-color: #7400A1">　　　</p>   | PANSY                      | <span style="white-space:nowrap">Pansy</span>        | #7400A1   | 116,0,161      | 283,100,63     |
| css      | <p style="background-color: #FFEFD5">　　　</p>   | PAPAYA_WHIP                | <span style="white-space:nowrap">Papaya Whip</span>         | #FFEFD5   | 255,239,213    | 37,16,100      |
| css      | <p style="background-color: #800080">　　　</p>   | PATRIARCH                  | <span style="white-space:nowrap">Patriarch</span>         | #800080   | 128,0,128      | 300,100,50     |
| web      | <p style="background-color: #FFE5B4">　　　</p>   | PEACH                      | <span style="white-space:nowrap">Peach</span>           | #FFE5B4   | 255,229,180    | 39,29,100      |
| web      | <p style="background-color: #FBBEA1">　　　</p>   | PEACH_PEARL                | <span style="white-space:nowrap">Peach Pearl</span>         | #FBBEA1   | 251,190,161    | 40,29,100      |
| css      | <p style="background-color: #FFDAB9">　　　</p>   | PEACH_PUFF                 | <span style="white-space:nowrap">Peach Puff</span>         | #FFDAB9   | 255,218,185    | 28,27,100      |
| web      | <p style="background-color: #00808C">　　　</p>   | PEACOCK_BLUE               | <span style="white-space:nowrap">Peacock Blue</span>         | #00808C   | 0,128,140      | 185,100,55     |
| web      | <p style="background-color: #00A15C">　　　</p>   | PEACOCK_GREEN              | <span style="white-space:nowrap">Peacock Green</span>         | #00A15C   | 0,161,92       | 154,100,63     |
| web      | <p style="background-color: #FFB3E6">　　　</p>   | PEARL_PINK                 | <span style="white-space:nowrap">Pearl Pink</span>        | #FFB3E6   | 255,179,230    | 320,30,100     |
| web      | <p style="background-color: #CCCCFF">　　　</p>   | PERIWINKLE                 | <span style="white-space:nowrap">Lavender Blue / Periwinkle</span>  | #CCCCFF   | 204,204,255    | 240,20,100     |
| web      | <p style="background-color: #FF4D40">　　　</p>   | PERSIMMON                  | <span style="white-space:nowrap">Persimmon</span>         | #FF4D40   | 255,77,64      | 4,75,100       |
| css      | <p style="background-color: #CD853F">　　　</p>   | PERU                       | <span style="white-space:nowrap">Peru</span>          | #CD853F   | 205,133,63     | 30,69,80       |
| css      | <p style="background-color: #FFC0CB">　　　</p>   | PINK                       | <span style="white-space:nowrap">Pink</span>          | #FFC0CB   | 255,192,203    | 350,25,100     |
| material | <p style="background-color: #FCE4EC">　　　</p>   | PINK_50                    | <span style="white-space:nowrap">Pink (50)</span>     | #FCE4EC   | 252,228,236    | 340,10,99      |
| material | <p style="background-color: #F8BBD0">　　　</p>   | PINK_100                   | <span style="white-space:nowrap">Pink (100)</span>    | #F8BBD0   | 248,187,208    | 339,25,97      |
| material | <p style="background-color: #F48FB1">　　　</p>   | PINK_200                   | <span style="white-space:nowrap">Pink (200)</span>    | #F48FB1   | 244,143,177    | 340,41,96      |
| material | <p style="background-color: #F06292">　　　</p>   | PINK_300                   | <span style="white-space:nowrap">Pink (300)</span>    | #F06292   | 240,98,146     | 340,59,94      |
| material | <p style="background-color: #EC407A">　　　</p>   | PINK_400                   | <span style="white-space:nowrap">Pink (400)</span>    | #EC407A   | 236,64,122     | 340,73,93      |
| material | <p style="background-color: #E91E63">　　　</p>   | PINK_500                   | <span style="white-space:nowrap">Pink (500)</span>    | #E91E63   | 233,30,99      | 340,87,91      |
| material | <p style="background-color: #D81B60">　　　</p>   | PINK_600                   | <span style="white-space:nowrap">Pink (600)</span>    | #D81B60   | 216,27,96      | 338,88,85      |
| material | <p style="background-color: #C2185B">　　　</p>   | PINK_700                   | <span style="white-space:nowrap">Pink (700)</span>    | #C2185B   | 194,24,91      | 336,88,76      |
| material | <p style="background-color: #AD1457">　　　</p>   | PINK_800                   | <span style="white-space:nowrap">Pink (800)</span>    | #AD1457   | 173,20,87      | 334,88,68      |
| material | <p style="background-color: #880E4F">　　　</p>   | PINK_900                   | <span style="white-space:nowrap">Pink (900)</span>    | #880E4F   | 136,14,79      | 328,90,53      |
| material | <p style="background-color: #FF80AB">　　　</p>   | PINK_A100                  | <span style="white-space:nowrap">Pink (A100)</span>   | #FF80AB   | 255,128,171    | 340,50,100     |
| material | <p style="background-color: #FF4081">　　　</p>   | PINK_A200                  | <span style="white-space:nowrap">Pink (A200)</span>   | #FF4081   | 255,64,129     | 340,75,100     |
| material | <p style="background-color: #F50057">　　　</p>   | PINK_A400                  | <span style="white-space:nowrap">Pink (A400)</span>   | #F50057   | 245,0,87       | 339,100,96     |
| material | <p style="background-color: #C51162">　　　</p>   | PINK_A700                  | <span style="white-space:nowrap">Pink (A700)</span>   | #C51162   | 197,17,98      | 333,91,77      |
| web      | <p style="background-color: #8E4585">　　　</p>   | PLUM                       | <span style="white-space:nowrap">Medium Lavender Magenta</span>          | #8E4585   | 142,69,133     | 307,51,56      |
| css      | <p style="background-color: #B0E0E6">　　　</p>   | POWDER_BLUE                | <span style="white-space:nowrap">Powder Blue</span>          | #B0E0E6   | 176,224,230    | 187,23,90      |
| web      | <p style="background-color: #003153">　　　</p>   | PRUSSIAN_BLUE              | <span style="white-space:nowrap">Prussian Blue</span>        | #003153   | 0,49,83        | 205,100,43     |
| android  | <p style="background-color: #800080">　　　</p>   | PURPLE                     | <span style="white-space:nowrap">Purple</span>           | #800080   | 128,0,128      | 300,100,50     |
| material | <p style="background-color: #F3E5F5">　　　</p>   | PURPLE_50                  | <span style="white-space:nowrap">Purple (50)</span>      | #F3E5F5   | 243,229,245    | 293,7,96       |
| material | <p style="background-color: #E1BEE7">　　　</p>   | PURPLE_100                 | <span style="white-space:nowrap">Purple (100)</span>     | #E1BEE7   | 225,190,231    | 291,18,91      |
| material | <p style="background-color: #CE93D8">　　　</p>   | PURPLE_200                 | <span style="white-space:nowrap">Purple (200)</span>     | #CE93D8   | 206,147,216    | 291,32,85      |
| material | <p style="background-color: #BA68C8">　　　</p>   | PURPLE_300                 | <span style="white-space:nowrap">Purple (300)</span>     | #BA68C8   | 186,104,200    | 291,48,78      |
| material | <p style="background-color: #AB47BC">　　　</p>   | PURPLE_400                 | <span style="white-space:nowrap">Purple (400)</span>     | #AB47BC   | 171,71,188     | 291,62,74      |
| material | <p style="background-color: #9C27B0">　　　</p>   | PURPLE_500                 | <span style="white-space:nowrap">Purple (500)</span>     | #9C27B0   | 156,39,176     | 291,78,69      |
| material | <p style="background-color: #8E24AA">　　　</p>   | PURPLE_600                 | <span style="white-space:nowrap">Purple (600)</span>     | #8E24AA   | 142,36,170     | 287,79,67      |
| material | <p style="background-color: #7B1FA2">　　　</p>   | PURPLE_700                 | <span style="white-space:nowrap">Purple (700)</span>     | #7B1FA2   | 123,31,162     | 282,81,64      |
| material | <p style="background-color: #6A1B9A">　　　</p>   | PURPLE_800                 | <span style="white-space:nowrap">Purple (800)</span>     | #6A1B9A   | 106,27,154     | 277,82,60      |
| material | <p style="background-color: #4A148C">　　　</p>   | PURPLE_900                 | <span style="white-space:nowrap">Purple (900)</span>     | #4A148C   | 74,20,140      | 267,86,55      |
| material | <p style="background-color: #EA80FC">　　　</p>   | PURPLE_A100                | <span style="white-space:nowrap">Purple (A100)</span>    | #EA80FC   | 234,128,252    | 291,49,99      |
| material | <p style="background-color: #E040FB">　　　</p>   | PURPLE_A200                | <span style="white-space:nowrap">Purple (A200)</span>    | #E040FB   | 224,64,251     | 291,75,98      |
| material | <p style="background-color: #D500F9">　　　</p>   | PURPLE_A400                | <span style="white-space:nowrap">Purple (A400)</span>    | #D500F9   | 213,0,249      | 291,100,98     |
| material | <p style="background-color: #AA00FF">　　　</p>   | PURPLE_A700                | <span style="white-space:nowrap">Purple (A700)</span>    | #AA00FF   | 170,0,255      | 280,100,100    |
| css      | <p style="background-color: #663399">　　　</p>   | REBECCA_PURPLE             | <span style="white-space:nowrap">Rebecca Purple</span>        | #663399   | 102,51,153     | 270,67,60      |
| android  | <p style="background-color: #FF0000">　　　</p>   | RED                        | <span style="white-space:nowrap">Red</span>           | #FF0000   | 255,0,0        | 0,100,100      |
| material | <p style="background-color: #FFEBEE">　　　</p>   | RED_50                     | <span style="white-space:nowrap">Red (50)</span>      | #FFEBEE   | 255,235,238    | 351,8,100      |
| material | <p style="background-color: #FFCDD2">　　　</p>   | RED_100                    | <span style="white-space:nowrap">Red (100)</span>     | #FFCDD2   | 255,205,210    | 354,20,100     |
| material | <p style="background-color: #EF9A9A">　　　</p>   | RED_200                    | <span style="white-space:nowrap">Red (200)</span>     | #EF9A9A   | 239,154,154    | 0,36,94        |
| material | <p style="background-color: #E57373">　　　</p>   | RED_300                    | <span style="white-space:nowrap">Red (300)</span>     | #E57373   | 229,115,115    | 0,50,90        |
| material | <p style="background-color: #EF5350">　　　</p>   | RED_400                    | <span style="white-space:nowrap">Red (400)</span>     | #EF5350   | 239,83,80      | 1,67,94        |
| material | <p style="background-color: #F44336">　　　</p>   | RED_500                    | <span style="white-space:nowrap">Red (500)</span>     | #F44336   | 244,67,54      | 4,78,96        |
| material | <p style="background-color: #E53935">　　　</p>   | RED_600                    | <span style="white-space:nowrap">Red (600)</span>     | #E53935   | 229,57,53      | 1,77,90        |
| material | <p style="background-color: #D32F2F">　　　</p>   | RED_700                    | <span style="white-space:nowrap">Red (700)</span>     | #D32F2F   | 211,47,47      | 0,78,83        |
| material | <p style="background-color: #C62828">　　　</p>   | RED_800                    | <span style="white-space:nowrap">Red (800)</span>     | #C62828   | 198,40,40      | 0,80,78        |
| material | <p style="background-color: #B71C1C">　　　</p>   | RED_900                    | <span style="white-space:nowrap">Red (900)</span>     | #B71C1C   | 183,28,28      | 0,85,72        |
| material | <p style="background-color: #FF8A80">　　　</p>   | RED_A100                   | <span style="white-space:nowrap">Red (A100)</span>    | #FF8A80   | 255,138,128    | 5,50,100       |
| material | <p style="background-color: #FF5252">　　　</p>   | RED_A200                   | <span style="white-space:nowrap">Red (A200)</span>    | #FF5252   | 255,82,82      | 0,68,100       |
| material | <p style="background-color: #FF1744">　　　</p>   | RED_A400                   | <span style="white-space:nowrap">Red (A400)</span>    | #FF1744   | 255,23,68      | 348,91,100     |
| material | <p style="background-color: #D50000">　　　</p>   | RED_A700                   | <span style="white-space:nowrap">Red (A700)</span>    | #D50000   | 213,0,0        | 0,100,84       |
| web      | <p style="background-color: #FF007F">　　　</p>   | ROSE                       | <span style="white-space:nowrap">Rose</span>         | #FF007F   | 255,0,127      | 330,100,100    |
| web      | <p style="background-color: #FF66CC">　　　</p>   | ROSE_PINK                  | <span style="white-space:nowrap">Rose Pink</span>        | #FF66CC   | 255,102,204    | 320,60,100     |
| css      | <p style="background-color: #BC8F8F">　　　</p>   | ROSY_BROWN                 | <span style="white-space:nowrap">Rosy Brown</span>         | #BC8F8F   | 188,143,143    | 0,24,74        |
| css      | <p style="background-color: #4169E1">　　　</p>   | ROYAL_BLUE                 | <span style="white-space:nowrap">Royal Blue</span>    | #4169E1   | 65,105,225     | 225,71,88      |
| web      | <p style="background-color: #CC0080">　　　</p>   | RUBY                       | <span style="white-space:nowrap">Ruby</span>         | #CC0080   | 204,0,128      | 322,100,80     |
| css      | <p style="background-color: #8B4513">　　　</p>   | SADDLE_BROWN               | <span style="white-space:nowrap">Saddle Brown</span>          | #8B4513   | 139,69,19      | 25,86,55       |
| css      | <p style="background-color: #FA8072">　　　</p>   | SALMON                     | <span style="white-space:nowrap">Salmon</span>          | #FA8072   | 250,128,114    | 6,54,98        |
| web      | <p style="background-color: #FF8099">　　　</p>   | SALMON_PINK                | <span style="white-space:nowrap">Salmon Pink</span>         | #FF8099   | 255,128,153    | 348,50,100     |
| web      | <p style="background-color: #4D80E6">　　　</p>   | SALVIA_BLUE                | <span style="white-space:nowrap">Salvia Blue</span>        | #4D80E6   | 77,128,230     | 220,67,90      |
| web      | <p style="background-color: #E6C3C3">　　　</p>   | SAND_BEIGE                 | <span style="white-space:nowrap">Sand Beige</span>          | #E6C3C3   | 230,195,195    | 0,15,90        |
| css      | <p style="background-color: #F4A460">　　　</p>   | SAND_BROWN                 | <span style="white-space:nowrap">Sandy Brown</span>          | #F4A460   | 244,164,96     | 28,61,96       |
| web      | <p style="background-color: #082567">　　　</p>   | SAPPHIRE                   | <span style="white-space:nowrap">Sapphire</span>    | #082567   | 8,37,103       | 222,92,40      |
| web      | <p style="background-color: #4798B3">　　　</p>   | SAXE_BLUE                  | <span style="white-space:nowrap">Saxe Blue</span>        | #4798B3   | 71,152,179     | 195,60,70      |
| web      | <p style="background-color: #FF2400">　　　</p>   | SCARLET                    | <span style="white-space:nowrap">Scarlet</span>     | #FF2400   | 255,36,0       | 8,100,100      |
| css      | <p style="background-color: #FFF5EE">　　　</p>   | SEASHELL                   | <span style="white-space:nowrap">Seashell</span>          | #FFF5EE   | 255,245,238    | 25,7,100       |
| css      | <p style="background-color: #2E8B57">　　　</p>   | SEA_GREEN                  | <span style="white-space:nowrap">Sea Green</span>          | #2E8B57   | 46,139,87      | 146,67,55      |
| web      | <p style="background-color: #704214">　　　</p>   | SEPIA                      | <span style="white-space:nowrap">Sepia</span>    | #704214   | 112,66,20      | 30,82,44       |
| web      | <p style="background-color: #FFB3BF">　　　</p>   | SHELL_PINK                 | <span style="white-space:nowrap">Shell Pink</span>         | #FFB3BF   | 255,179,191    | 351,30,100     |
| css      | <p style="background-color: #A0522D">　　　</p>   | SIENNA                     | <span style="white-space:nowrap">Sienna</span>          | #A0522D   | 160,82,45      | 19,72,63       |
| android  | <p style="background-color: #C0C0C0">　　　</p>   | SILVER                     | <span style="white-space:nowrap">Silver</span>           | #C0C0C0   | 192,192,192    | 0,0,75         |
| css      | <p style="background-color: #87CEEB">　　　</p>   | SKY_BLUE                   | <span style="white-space:nowrap">Sky Blue</span>         | #87CEEB   | 135,206,235    | 197,43,92      |
| css      | <p style="background-color: #6A5ACD">　　　</p>   | SLATE_BLUE                 | <span style="white-space:nowrap">Slate Blue</span>          | #6A5ACD   | 106,90,205     | 248,56,80      |
| css      | <p style="background-color: #708090">　　　</p>   | SLATE_GRAY                 | <span style="white-space:nowrap">Slate Gray</span>          | #708090   | 112,128,144    | 210,22,56      |
| css      | <p style="background-color: #708090">　　　</p>   | SLATE_GREY                 | <span style="white-space:nowrap">Slate Gray</span>          | #708090   | 112,128,144    | 210,22,56      |
| css      | <p style="background-color: #FFFAFA">　　　</p>   | SNOW                       | <span style="white-space:nowrap">Snow</span>           | #FFFAFA   | 255,250,250    | 0,2,100        |
| web      | <p style="background-color: #FF73B3">　　　</p>   | SPINEL_RED                 | <span style="white-space:nowrap">Spinel Red</span>        | #FF73B3   | 255,115,179    | 333,55,100     |
| css      | <p style="background-color: #00FF7F">　　　</p>   | SPRING_GREEN               | <span style="white-space:nowrap">Spring Green</span>          | #00FF7F   | 0,255,127      | 150,100,100    |
| css      | <p style="background-color: #4682B4">　　　</p>   | STEEL_BLUE                 | <span style="white-space:nowrap">Steel Blue</span>          | #4682B4   | 70,130,180     | 207,61,71      |
| web      | <p style="background-color: #006374">　　　</p>   | STRONG_BLUE                | <span style="white-space:nowrap">Strong Blue</span>          | #006374   | 0,99,116       | 189,100,45     |
| web      | <p style="background-color: #E60000">　　　</p>   | STRONG_RED                 | <span style="white-space:nowrap">Strong Red</span>          | #E60000   | 230,0,0        | 0,100,90       |
| web      | <p style="background-color: #FF7300">　　　</p>   | SUN_ORANGE                 | <span style="white-space:nowrap">Sun Orange</span>          | #FF7300   | 255,115,0      | 27,100,100     |
| css      | <p style="background-color: #D2B48C">　　　</p>   | TAN                        | <span style="white-space:nowrap">Tan</span>          | #D2B48C   | 210,180,140    | 34,33,82       |
| web      | <p style="background-color: #F28500">　　　</p>   | TANGERINE                  | <span style="white-space:nowrap">Tangerine</span>           | #F28500   | 242,133,0      | 33,100,95      |
| web      | <p style="background-color: #FFCC00">　　　</p>   | TANGERINE_YELLOW           | <span style="white-space:nowrap">Tangerine Yellow</span>          | #FFCC00   | 255,204,0      | 48,100,100     |
| android  | <p style="background-color: #008080">　　　</p>   | TEAL                       | <span style="white-space:nowrap">Teal</span>     | #008080   | 0,128,128      | 180,100,50     |
| material | <p style="background-color: #E0F2F1">　　　</p>   | TEAL_50                    | <span style="white-space:nowrap">Teal (50)</span>     | #E0F2F1   | 224,242,241    | 177,7,95       |
| material | <p style="background-color: #B2DFDB">　　　</p>   | TEAL_100                   | <span style="white-space:nowrap">Teal (100)</span>    | #B2DFDB   | 178,223,219    | 175,20,87      |
| material | <p style="background-color: #80CBC4">　　　</p>   | TEAL_200                   | <span style="white-space:nowrap">Teal (200)</span>    | #80CBC4   | 128,203,196    | 174,37,80      |
| material | <p style="background-color: #4DB6AC">　　　</p>   | TEAL_300                   | <span style="white-space:nowrap">Teal (300)</span>    | #4DB6AC   | 77,182,172     | 174,58,71      |
| material | <p style="background-color: #26A69A">　　　</p>   | TEAL_400                   | <span style="white-space:nowrap">Teal (400)</span>    | #26A69A   | 38,166,154     | 174,77,65      |
| material | <p style="background-color: #009688">　　　</p>   | TEAL_500                   | <span style="white-space:nowrap">Teal (500)</span>    | #009688   | 0,150,136      | 174,100,59     |
| material | <p style="background-color: #00897B">　　　</p>   | TEAL_600                   | <span style="white-space:nowrap">Teal (600)</span>    | #00897B   | 0,137,123      | 174,100,54     |
| material | <p style="background-color: #00796B">　　　</p>   | TEAL_700                   | <span style="white-space:nowrap">Teal (700)</span>    | #00796B   | 0,121,107      | 173,100,47     |
| material | <p style="background-color: #00695C">　　　</p>   | TEAL_800                   | <span style="white-space:nowrap">Teal (800)</span>    | #00695C   | 0,105,92       | 173,100,41     |
| material | <p style="background-color: #004D40">　　　</p>   | TEAL_900                   | <span style="white-space:nowrap">Teal (900)</span>    | #004D40   | 0,77,64        | 170,100,30     |
| material | <p style="background-color: #A7FFEB">　　　</p>   | TEAL_A100                  | <span style="white-space:nowrap">Teal (A100)</span>   | #A7FFEB   | 167,255,235    | 166,35,100     |
| material | <p style="background-color: #64FFDA">　　　</p>   | TEAL_A200                  | <span style="white-space:nowrap">Teal (A200)</span>   | #64FFDA   | 100,255,218    | 166,61,100     |
| material | <p style="background-color: #1DE9B6">　　　</p>   | TEAL_A400                  | <span style="white-space:nowrap">Teal (A400)</span>   | #1DE9B6   | 29,233,182     | 165,88,91      |
| material | <p style="background-color: #00BFA5">　　　</p>   | TEAL_A700                  | <span style="white-space:nowrap">Teal (A700)</span>   | #00BFA5   | 0,191,165      | 172,100,75     |
| css      | <p style="background-color: #D8BFD8">　　　</p>   | THISTLE                    | <span style="white-space:nowrap">Thistle</span>          | #D8BFD8   | 216,191,216    | 300,12,85      |
| css      | <p style="background-color: #FF6347">　　　</p>   | TOMATO                     | <span style="white-space:nowrap">Tomato</span>         | #FF6347   | 255,99,71      | 9,72,100       |
| android  | <p style="background-color: #00000000">　　　</p> | TRANSPARENT                | <span style="white-space:nowrap">Transparent</span>          | #00000000 | 0,0,0,0 (RGBA) | 0,0,0,0 (HSVA) |
| web      | <p style="background-color: #FF8033">　　　</p>   | TROPICAL_ORANGE            | <span style="white-space:nowrap">Tropical Orange</span>         | #FF8033   | 255,128,51     | 23,80,100      |
| css      | <p style="background-color: #40E0D0">　　　</p>   | TURQUOISE                  | <span style="white-space:nowrap">Turquoise</span>          | #40E0D0   | 64,224,208     | 174,71,88      |
| web      | <p style="background-color: #00FFEF">　　　</p>   | TURQUOISE_BLUE             | <span style="white-space:nowrap">Turquoise Blue</span>        | #00FFEF   | 0,255,239      | 176,100,100    |
| web      | <p style="background-color: #4DE680">　　　</p>   | TURQUOISE_GREEN            | <span style="white-space:nowrap">Turquoise Green</span>        | #4DE680   | 77,230,128     | 140,67,90      |
| web      | <p style="background-color: #0033FF">　　　</p>   | ULTRAMARINE                | <span style="white-space:nowrap">Ultramarine</span>        | #0033FF   | 0,51,255       | 228,100,100    |
| web      | <p style="background-color: #E34234">　　　</p>   | VERMILION                  | <span style="white-space:nowrap">Vermilion</span>          | #E34234   | 227,66,52      | 5,77,89        |
| web      | <p style="background-color: #73E68C">　　　</p>   | VERY_LIGHT_MALACHITE_GREEN | <span style="white-space:nowrap">Malachite</span>        | #73E68C   | 115,230,140    | 133,50,90      |
| css      | <p style="background-color: #EE82EE">　　　</p>   | VIOLET                     | <span style="white-space:nowrap">Violet</span>         | #EE82EE   | 238,130,238    | 300,45,93      |
| web      | <p style="background-color: #127436">　　　</p>   | VIRIDIAN                   | <span style="white-space:nowrap">Viridian</span>          | #127436   | 18,116,54      | 142,84,45      |
| web      | <p style="background-color: #5686BF">　　　</p>   | WEDGWOOD_BLUE              | <span style="white-space:nowrap">Wedgwood Blue</span>      | #5686BF   | 86,134,191     | 213,55,75      |
| css      | <p style="background-color: #F5DEB3">　　　</p>   | WHEAT                      | <span style="white-space:nowrap">Wheat</span>          | #F5DEB3   | 245,222,179    | 39,27,96       |
| android  | <p style="background-color: #FFFFFF">　　　</p>   | WHITE                      | <span style="white-space:nowrap">White</span>           | #FFFFFF   | 255,255,255    | 0,0,100        |
| material | <p style="background-color: #FFFFFF">　　　</p>   | WHITE_1000                 | <span style="white-space:nowrap">White</span>           | #FFFFFF   | 255,255,255    | 0,0,100        |
| css      | <p style="background-color: #F5F5F5">　　　</p>   | WHITE_SMOKE                | <span style="white-space:nowrap">White Smoke</span>          | #F5F5F5   | 245,245,245    | 0,0,96         |
| web      | <p style="background-color: #C9A0DC">　　　</p>   | WISTERIA                   | <span style="white-space:nowrap">Wisteria</span>          | #C9A0DC   | 201,160,220    | 281,27,86      |
| android  | <p style="background-color: #FFFF00">　　　</p>   | YELLOW                     | <span style="white-space:nowrap">Yellow</span>           | #FFFF00   | 255,255,0      | 60,100,100     |
| material | <p style="background-color: #FFFDE7">　　　</p>   | YELLOW_50                  | <span style="white-space:nowrap">Yellow (50)</span>      | #FFFDE7   | 255,253,231    | 55,9,100       |
| material | <p style="background-color: #FFF9C4">　　　</p>   | YELLOW_100                 | <span style="white-space:nowrap">Yellow (100)</span>     | #FFF9C4   | 255,249,196    | 54,23,100      |
| material | <p style="background-color: #FFF590">　　　</p>   | YELLOW_200                 | <span style="white-space:nowrap">Yellow (200)</span>     | #FFF590   | 255,245,144    | 55,44,100      |
| material | <p style="background-color: #FFF176">　　　</p>   | YELLOW_300                 | <span style="white-space:nowrap">Yellow (300)</span>     | #FFF176   | 255,241,118    | 54,54,100      |
| material | <p style="background-color: #FFEE58">　　　</p>   | YELLOW_400                 | <span style="white-space:nowrap">Yellow (400)</span>     | #FFEE58   | 255,238,88     | 54,65,100      |
| material | <p style="background-color: #FFEB3B">　　　</p>   | YELLOW_500                 | <span style="white-space:nowrap">Yellow (500)</span>     | #FFEB3B   | 255,235,59     | 54,77,100      |
| material | <p style="background-color: #FDD835">　　　</p>   | YELLOW_600                 | <span style="white-space:nowrap">Yellow (600)</span>     | #FDD835   | 253,216,53     | 49,79,99       |
| material | <p style="background-color: #FBC02D">　　　</p>   | YELLOW_700                 | <span style="white-space:nowrap">Yellow (700)</span>     | #FBC02D   | 251,192,45     | 43,82,98       |
| material | <p style="background-color: #F9A825">　　　</p>   | YELLOW_800                 | <span style="white-space:nowrap">Yellow (800)</span>     | #F9A825   | 249,168,37     | 37,85,98       |
| material | <p style="background-color: #F57F17">　　　</p>   | YELLOW_900                 | <span style="white-space:nowrap">Yellow (900)</span>     | #F57F17   | 245,127,23     | 28,91,96       |
| material | <p style="background-color: #FFFF82">　　　</p>   | YELLOW_A100                | <span style="white-space:nowrap">Yellow (A100)</span>    | #FFFF82   | 255,255,130    | 60,49,100      |
| material | <p style="background-color: #FFFF00">　　　</p>   | YELLOW_A200                | <span style="white-space:nowrap">Yellow (A200)</span>    | #FFFF00   | 255,255,0      | 60,100,100     |
| material | <p style="background-color: #FFEA00">　　　</p>   | YELLOW_A400                | <span style="white-space:nowrap">Yellow (A400)</span>    | #FFEA00   | 255,234,0      | 55,100,100     |
| material | <p style="background-color: #FFD600">　　　</p>   | YELLOW_A700                | <span style="white-space:nowrap">Yellow (A700)</span>    | #FFD600   | 255,214,0      | 50,100,100     |
| css      | <p style="background-color: #9ACD32">　　　</p>   | YELLOW_GREEN               | <span style="white-space:nowrap">Yellow Green</span>          | #9ACD32   | 154,205,50     | 80,76,80       |

All color entries in the fused list support the `colors.NAME` or `'NAME'` color name access methods:

```js
/* Red, get its RGB component array. */
colors.toRgb(colors.RED);
colors.toRgb('RED');

/* Coffee color, get its color integer. */
colors.toInt(colors.COFFEE);
colors.toInt('COFFEE');

/* Material 700 Amber color, get its Hex code. */
colors.toHex(colors.AMBER_700);
colors.toHex('AMBER_700');
```