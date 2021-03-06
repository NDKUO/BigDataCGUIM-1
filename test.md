NBA 2014-2015球季 各隊分析
================

``` r
#install.packages("SportsAnalytics")
library(SportsAnalytics)
```

    ## Warning: package 'SportsAnalytics' was built under R version 3.2.4

``` r
NBA1415<-fetch_NBAPlayerStatistics("14-15")
```

各隊最辛苦的球員
----------------

計算依據為各隊全季總出場分鐘數最多的球員

``` r
MaxMinutesPlayed<-aggregate(TotalMinutesPlayed~Team,NBA1415,max)
NBA1415MaxMinutesPlayed<-merge(NBA1415,MaxMinutesPlayed)
output<-NBA1415MaxMinutesPlayed[order(NBA1415MaxMinutesPlayed$TotalMinutesPlayed,decreasing = T),c("Team","Name","TotalMinutesPlayed")]
library(knitr)
kable(output, digits=2)
```

|     | Team | Name             |  TotalMinutesPlayed|
|-----|:-----|:-----------------|-------------------:|
| 11  | HOU  | James Harden     |                2979|
| 18  | MIN  | Andrew Wiggins   |                2971|
| 25  | POR  | Damian Lillard   |                2928|
| 13  | LAC  | Chris Paul       |                2860|
| 30  | WAS  | John Wall        |                2841|
| 24  | PHO  | Eric Bledsoe     |                2799|
| 3   | BRO  | Joe Johnson      |                2787|
| 6   | CLE  | Kyrie Irving     |                2735|
| 7   | DAL  | Monta Ellis      |                2698|
| 19  | NOR  | Tyreke Evans     |                2695|
| 15  | MEM  | Marc Gasol       |                2690|
| 5   | CHI  | Pau Gasol        |                2682|
| 26  | SAC  | Ben Mclemore     |                2674|
| 8   | DEN  | Ty Lawson        |                2668|
| 16  | MIA  | Goran Dragic     |                2641|
| 29  | UTA  | Gordon Hayward   |                2618|
| 10  | GSW  | Stephen Curry    |                2613|
| 9   | DET  | Ke Caldwell-pope |                2591|
| 22  | ORL  | Victor Oladipo   |                2572|
| 17  | MIL  | G Antetokounmpo  |                2542|
| 2   | BOS  | Avery Bradley    |                2427|
| 28  | TOR  | Kyle Lowry       |                2422|
| 1   | ATL  | Kyle Korver      |                2418|
| 12  | IND  | Solomon Hill     |                2380|
| 4   | CHA  | Gerald Henderson |                2323|
| 23  | PHI  | Nerlens Noel     |                2311|
| 27  | SAN  | Danny Green      |                2311|
| 21  | OKL  | Russel Westbrook |                2302|
| 14  | LAL  | Wesley Johnson   |                2244|
| 20  | NYK  | Shane Larkin     |                1864|

各隊得分王
----------

計算依據為各隊全季總得分最多的球員

``` r
MaxPoint<-aggregate(TotalPoints~Team,NBA1415,max)
#tapply(NBA1415$TotalPoints,NBA1415$Team,max)
NBA1415MaxPoint<-merge(NBA1415,MaxPoint)
output<-NBA1415MaxPoint[order(NBA1415MaxPoint$TotalPoints,decreasing = T),c("Team","Name","TotalPoints")]
library(knitr)
kable(output, digits=2)
```

|     | Team | Name             |  TotalPoints|
|-----|:-----|:-----------------|------------:|
| 11  | HOU  | James Harden     |         2217|
| 10  | GSW  | Stephen Curry    |         1900|
| 21  | OKL  | Russel Westbrook |         1886|
| 6   | CLE  | Lebron James     |         1740|
| 25  | POR  | Damian Lillard   |         1720|
| 19  | NOR  | Anthony Davis    |         1656|
| 13  | LAC  | Chris Paul       |         1564|
| 7   | DAL  | Monta Ellis      |         1513|
| 29  | UTA  | Gordon Hayward   |         1463|
| 5   | CHI  | Pau Gasol        |         1446|
| 26  | SAC  | Rudy Gay         |         1432|
| 22  | ORL  | Nikola Vucevic   |         1428|
| 15  | MEM  | Marc Gasol       |         1413|
| 18  | MIN  | Andrew Wiggins   |         1387|
| 30  | WAS  | John Wall        |         1385|
| 24  | PHO  | Eric Bledsoe     |         1377|
| 16  | MIA  | Dwyane Wade      |         1331|
| 28  | TOR  | Kyle Lowry       |         1244|
| 3   | BRO  | Brook Lopez      |         1236|
| 1   | ATL  | Paul Millsap     |         1218|
| 8   | DEN  | Ty Lawson        |         1143|
| 9   | DET  | Andre Drummond   |         1130|
| 2   | BOS  | Isaiah Thomas    |         1101|
| 4   | CHA  | Al Jefferson     |         1080|
| 27  | SAN  | Tim Duncan       |         1070|
| 17  | MIL  | Khris Middleton  |         1055|
| 20  | NYK  | Carmelo Anthony  |          966|
| 12  | IND  | C.j. Miles       |          942|
| 23  | PHI  | Robert Covington |          927|
| 14  | LAL  | Jordan Hill      |          841|

各隊最有效率的球員
------------------

計算依據為（各隊全季總得分/ 出戰分鐘數）最高的球員

``` r
Efficiency <- NBA1415$TotalPoints / NBA1415$TotalMinutesPlayed
NBA1415Efficiency<-cbind(NBA1415,Efficiency)
MaxEfficiency<-aggregate(Efficiency~Team,NBA1415Efficiency,max)
NBA1415MaxEfficiency<-merge(NBA1415,MaxEfficiency)
output3<-NBA1415MaxEfficiency[order(NBA1415MaxEfficiency$Efficiency,decreasing = T),c("Team","Name","Efficiency")]
library(knitr)
kable(output3, digits=2)
```

|     | Team | Name               |  Efficiency|
|-----|:-----|:-------------------|-----------:|
| 330 | OKL  | Sebastia Telfair   |        0.82|
| 331 | OKL  | Anthony Morrow     |        0.82|
| 332 | OKL  | Steven Adams       |        0.82|
| 333 | OKL  | Kyle Singler       |        0.82|
| 334 | OKL  | Dion Waiters       |        0.82|
| 335 | OKL  | Andre Roberson     |        0.82|
| 336 | OKL  | Enes Kanter        |        0.82|
| 337 | OKL  | Mitch Mcgary       |        0.82|
| 338 | OKL  | Nick Collison      |        0.82|
| 339 | OKL  | Kevin Durant       |        0.82|
| 340 | OKL  | Perry Jones        |        0.82|
| 341 | OKL  | Serge Ibaka        |        0.82|
| 342 | OKL  | Jeremy Lamb        |        0.82|
| 343 | OKL  | Russel Westbrook   |        0.82|
| 344 | OKL  | Steve Novak        |        0.82|
| 345 | OKL  | D.j. Augustin      |        0.82|
| 155 | HOU  | Corey Brewer       |        0.74|
| 156 | HOU  | Donat Motiejunas   |        0.74|
| 157 | HOU  | Kos Papanikolaou   |        0.74|
| 158 | HOU  | Nick Johnson       |        0.74|
| 159 | HOU  | Trevor Ariza       |        0.74|
| 160 | HOU  | K.j. Mcdaniels     |        0.74|
| 161 | HOU  | Jason Terry        |        0.74|
| 162 | HOU  | James Harden       |        0.74|
| 163 | HOU  | Clint Capela       |        0.74|
| 164 | HOU  | Patrick Beverley   |        0.74|
| 165 | HOU  | Francisco Garcia   |        0.74|
| 166 | HOU  | Josh Smith         |        0.74|
| 167 | HOU  | Pablo Prigioni     |        0.74|
| 168 | HOU  | Dwight Howard      |        0.74|
| 169 | HOU  | Terrence Jones     |        0.74|
| 170 | HOU  | Joey Dorsey        |        0.74|
| 140 | GSW  | Stephen Curry      |        0.73|
| 141 | GSW  | Andrew Bogut       |        0.73|
| 142 | GSW  | Justin Holiday     |        0.73|
| 143 | GSW  | Harrison Barnes    |        0.73|
| 144 | GSW  | James Mcadoo       |        0.73|
| 145 | GSW  | Draymond Green     |        0.73|
| 146 | GSW  | Andre Iguodala     |        0.73|
| 147 | GSW  | Shaun Livingston   |        0.73|
| 148 | GSW  | Brandon Rush       |        0.73|
| 149 | GSW  | Leandro Barbosa    |        0.73|
| 150 | GSW  | David Lee          |        0.73|
| 151 | GSW  | Marrees Speights   |        0.73|
| 152 | GSW  | Klay Thompson      |        0.73|
| 153 | GSW  | Festus Ezeli       |        0.73|
| 154 | GSW  | Ognjen Kuzmic      |        0.73|
| 412 | SAC  | Omri Casspi        |        0.71|
| 413 | SAC  | Demarcus Cousins   |        0.71|
| 414 | SAC  | Ray Mccallum       |        0.71|
| 415 | SAC  | Derrick Williams   |        0.71|
| 416 | SAC  | Eric Moreland      |        0.71|
| 417 | SAC  | Carl Landry        |        0.71|
| 418 | SAC  | Jason Thompson     |        0.71|
| 419 | SAC  | David Stockton     |        0.71|
| 420 | SAC  | Ryan Hollins       |        0.71|
| 421 | SAC  | Sim Bhullar        |        0.71|
| 422 | SAC  | David Wear         |        0.71|
| 423 | SAC  | Rudy Gay           |        0.71|
| 424 | SAC  | Andre Miller       |        0.71|
| 425 | SAC  | Darren Collison    |        0.71|
| 426 | SAC  | Nik Stauskas       |        0.71|
| 427 | SAC  | Ben Mclemore       |        0.71|
| 428 | SAC  | Reggie Evans       |        0.71|
| 78  | CLE  | Shawn Marion       |        0.70|
| 79  | CLE  | Tristan Thompson   |        0.70|
| 80  | CLE  | Lebron James       |        0.70|
| 81  | CLE  | Mike Miller        |        0.70|
| 82  | CLE  | Timofey Mozgov     |        0.70|
| 83  | CLE  | Will Cherry        |        0.70|
| 84  | CLE  | Brendan Haywood    |        0.70|
| 85  | CLE  | Kyrie Irving       |        0.70|
| 86  | CLE  | J.r. Smith         |        0.70|
| 87  | CLE  | Anderson Varejao   |        0.70|
| 88  | CLE  | Kevin Love         |        0.70|
| 89  | CLE  | Joe Harris         |        0.70|
| 90  | CLE  | Iman Shumpert      |        0.70|
| 91  | CLE  | James Jones        |        0.70|
| 92  | CLE  | Matt Dellavedova   |        0.70|
| 93  | CLE  | Alex Kirk          |        0.70|
| 314 | NYK  | Quincy Acy         |        0.68|
| 315 | NYK  | Langsto Galloway   |        0.68|
| 316 | NYK  | Shane Larkin       |        0.68|
| 317 | NYK  | Cole Aldrich       |        0.68|
| 318 | NYK  | Alexey Shved       |        0.68|
| 319 | NYK  | Carmelo Anthony    |        0.68|
| 320 | NYK  | Cleanthony Early   |        0.68|
| 321 | NYK  | Ricky Ledo         |        0.68|
| 322 | NYK  | Tim Hardaway       |        0.68|
| 323 | NYK  | Jose Calderon      |        0.68|
| 324 | NYK  | Travis Wear        |        0.68|
| 325 | NYK  | Lou Amundson       |        0.68|
| 326 | NYK  | Andrea Bargnani    |        0.68|
| 327 | NYK  | Jason Smith        |        0.68|
| 328 | NYK  | Lance Thomas       |        0.68|
| 329 | NYK  | Samuel Dalembert   |        0.68|
| 240 | MIA  | Luol Deng          |        0.67|
| 241 | MIA  | Chris Bosh         |        0.67|
| 242 | MIA  | James Ennis        |        0.67|
| 243 | MIA  | Josh Mcroberts     |        0.67|
| 244 | MIA  | Shannon Brown      |        0.67|
| 245 | MIA  | Hassan Whiteside   |        0.67|
| 246 | MIA  | Michael Beasley    |        0.67|
| 247 | MIA  | Henry Walker       |        0.67|
| 248 | MIA  | Goran Dragic       |        0.67|
| 249 | MIA  | Tyler Johnson      |        0.67|
| 250 | MIA  | Zoran Dragic       |        0.67|
| 251 | MIA  | Udonis Haslem      |        0.67|
| 252 | MIA  | Andre Dawkins      |        0.67|
| 253 | MIA  | Danny Granger      |        0.67|
| 254 | MIA  | Shabazz Napier     |        0.67|
| 255 | MIA  | Dwyane Wade        |        0.67|
| 256 | MIA  | Mario Chalmers     |        0.67|
| 257 | MIA  | Chris Andersen     |        0.67|
| 295 | NOR  | Jimmer Fredette    |        0.67|
| 296 | NOR  | Dante Cunningham   |        0.67|
| 297 | NOR  | Darius Miller      |        0.67|
| 298 | NOR  | Eric Gordon        |        0.67|
| 299 | NOR  | Ryan Anderson      |        0.67|
| 300 | NOR  | Alexis Ajinca      |        0.67|
| 301 | NOR  | Toney Douglas      |        0.67|
| 302 | NOR  | Quincy Pondexter   |        0.67|
| 303 | NOR  | Norris Cole        |        0.67|
| 304 | NOR  | Omer Asik          |        0.67|
| 305 | NOR  | John Salmons       |        0.67|
| 306 | NOR  | Gal Mekel          |        0.67|
| 307 | NOR  | Tyreke Evans       |        0.67|
| 308 | NOR  | Luke Babbitt       |        0.67|
| 309 | NOR  | Jrue Holiday       |        0.67|
| 310 | NOR  | Elliot Williams    |        0.67|
| 311 | NOR  | Anthony Davis      |        0.67|
| 312 | NOR  | Jeff Withey        |        0.67|
| 313 | NOR  | Nate Wolters       |        0.67|
| 223 | MEM  | Zach Randolph      |        0.67|
| 224 | MEM  | Kosta Koufos       |        0.67|
| 225 | MEM  | Russ Smith         |        0.67|
| 226 | MEM  | Jordan Adams       |        0.67|
| 227 | MEM  | Jarnell Stokes     |        0.67|
| 228 | MEM  | Marc Gasol         |        0.67|
| 229 | MEM  | Tony Allen         |        0.67|
| 230 | MEM  | Kalin Lucas        |        0.67|
| 231 | MEM  | Tyrus Thomas       |        0.67|
| 232 | MEM  | Jon Leuer          |        0.67|
| 233 | MEM  | Jamychal Green     |        0.67|
| 234 | MEM  | Beno Udrih         |        0.67|
| 235 | MEM  | Vince Carter       |        0.67|
| 236 | MEM  | Nick Calathes      |        0.67|
| 237 | MEM  | Jeff Green         |        0.67|
| 238 | MEM  | Mike Conley        |        0.67|
| 239 | MEM  | Courtney Lee       |        0.67|
| 396 | POR  | Tim Frazier        |        0.66|
| 397 | POR  | Nicolas Batum      |        0.66|
| 398 | POR  | C.j. Mccollum      |        0.66|
| 399 | POR  | Steve Blake        |        0.66|
| 400 | POR  | Lamarcu Aldridge   |        0.66|
| 401 | POR  | Robin Lopez        |        0.66|
| 402 | POR  | Arron Afflalo      |        0.66|
| 403 | POR  | Wesley Matthews    |        0.66|
| 404 | POR  | Dorell Wright      |        0.66|
| 405 | POR  | Alonzo Gee         |        0.66|
| 406 | POR  | Joel Freeland      |        0.66|
| 407 | POR  | Damian Lillard     |        0.66|
| 408 | POR  | Chris Kaman        |        0.66|
| 409 | POR  | Allen Crabbe       |        0.66|
| 410 | POR  | Meyers Leonard     |        0.66|
| 411 | POR  | Victor Claver      |        0.66|
| 205 | LAL  | Jordan Hill        |        0.65|
| 206 | LAL  | Ronnie Price       |        0.65|
| 207 | LAL  | Jordan Clarkson    |        0.65|
| 208 | LAL  | Dwight Buycks      |        0.65|
| 209 | LAL  | Jabari Brown       |        0.65|
| 210 | LAL  | Ed Davis           |        0.65|
| 211 | LAL  | Kobe Bryant        |        0.65|
| 212 | LAL  | Vander Blue        |        0.65|
| 213 | LAL  | Jeremy Lin         |        0.65|
| 214 | LAL  | Julius Randle      |        0.65|
| 215 | LAL  | Wesley Johnson     |        0.65|
| 216 | LAL  | Wayne Ellington    |        0.65|
| 217 | LAL  | Robert Sacre       |        0.65|
| 218 | LAL  | Tarik Black        |        0.65|
| 219 | LAL  | Ryan Kelly         |        0.65|
| 220 | LAL  | Nick Young         |        0.65|
| 221 | LAL  | Carlos Boozer      |        0.65|
| 222 | LAL  | Xavier Henry       |        0.65|
| 16  | BOS  | Luigi Datome       |        0.64|
| 17  | BOS  | Isaiah Thomas      |        0.64|
| 18  | BOS  | Tyler Zeller       |        0.64|
| 19  | BOS  | Shavlik Randolph   |        0.64|
| 20  | BOS  | Avery Bradley      |        0.64|
| 21  | BOS  | Evan Turner        |        0.64|
| 22  | BOS  | James Young        |        0.64|
| 23  | BOS  | Brandon Bass       |        0.64|
| 24  | BOS  | Jae Crowder        |        0.64|
| 25  | BOS  | Phil Pressey       |        0.64|
| 26  | BOS  | Jared Sullinger    |        0.64|
| 27  | BOS  | Marcus Smart       |        0.64|
| 28  | BOS  | Kelly Olynyk       |        0.64|
| 29  | BOS  | Gerald Wallace     |        0.64|
| 30  | BOS  | Jonas Jerebko      |        0.64|
| 186 | LAC  | Ekpe Udoh          |        0.62|
| 187 | LAC  | Jordan Hamilton    |        0.62|
| 188 | LAC  | Douglas-roberts    |        0.62|
| 189 | LAC  | C.j. Wilcox        |        0.62|
| 190 | LAC  | Matt Barnes        |        0.62|
| 191 | LAC  | Austin Rivers      |        0.62|
| 192 | LAC  | Dahntay Jones      |        0.62|
| 193 | LAC  | Lester Hudson      |        0.62|
| 194 | LAC  | Jordan Farmar      |        0.62|
| 195 | LAC  | Deandre Jordan     |        0.62|
| 196 | LAC  | Spencer Hawes      |        0.62|
| 197 | LAC  | Hedo Turkoglu      |        0.62|
| 198 | LAC  | Jared Cunningham   |        0.62|
| 199 | LAC  | Nate Robinson      |        0.62|
| 200 | LAC  | Chris Paul         |        0.62|
| 201 | LAC  | J.j. Redick        |        0.62|
| 202 | LAC  | Blake Griffin      |        0.62|
| 203 | LAC  | Glen Davis         |        0.62|
| 204 | LAC  | Jamal Crawford     |        0.62|
| 444 | TOR  | Bruno Caboclo      |        0.62|
| 445 | TOR  | Greivis Vasquez    |        0.62|
| 446 | TOR  | Chuck Hayes        |        0.62|
| 447 | TOR  | Terrence Ross      |        0.62|
| 448 | TOR  | Amir Johnson       |        0.62|
| 449 | TOR  | James Johnson      |        0.62|
| 450 | TOR  | Greg Stiemsma      |        0.62|
| 451 | TOR  | Landry Fields      |        0.62|
| 452 | TOR  | Demar Derozan      |        0.62|
| 453 | TOR  | Kyle Lowry         |        0.62|
| 454 | TOR  | Lucas Nogueira     |        0.62|
| 455 | TOR  | Patric Patterson   |        0.62|
| 456 | TOR  | Jona Valanciunas   |        0.62|
| 457 | TOR  | Tyler Hansbrough   |        0.62|
| 458 | TOR  | Louis Williams     |        0.62|
| 380 | PHO  | Alex Len           |        0.61|
| 381 | PHO  | Eric Bledsoe       |        0.61|
| 382 | PHO  | Brandon Knight     |        0.61|
| 383 | PHO  | Marcus Morris      |        0.61|
| 384 | PHO  | P.j. Tucker        |        0.61|
| 385 | PHO  | A.j. Price         |        0.61|
| 386 | PHO  | Seth Curry         |        0.61|
| 387 | PHO  | Reggie Bullock     |        0.61|
| 388 | PHO  | T.j. Warren        |        0.61|
| 389 | PHO  | Brandan Wright     |        0.61|
| 390 | PHO  | Markieff Morris    |        0.61|
| 391 | PHO  | Archie Goodwin     |        0.61|
| 392 | PHO  | Earl Barron        |        0.61|
| 393 | PHO  | Jerel Mcneal       |        0.61|
| 394 | PHO  | Gerald Green       |        0.61|
| 395 | PHO  | Marcus Thornton    |        0.61|
| 275 | MIN  | Zach Lavine        |        0.60|
| 276 | MIN  | Gary Neal          |        0.60|
| 277 | MIN  | Kevin Garnett      |        0.60|
| 278 | MIN  | Ricky Rubio        |        0.60|
| 279 | MIN  | Miros Raduljica    |        0.60|
| 280 | MIN  | Jeff Adrien        |        0.60|
| 281 | MIN  | Chase Budinger     |        0.60|
| 282 | MIN  | Kevin Martin       |        0.60|
| 283 | MIN  | Andrew Wiggins     |        0.60|
| 284 | MIN  | Gorgui Dieng       |        0.60|
| 285 | MIN  | Anthony Bennett    |        0.60|
| 286 | MIN  | Sean Kilpatrick    |        0.60|
| 287 | MIN  | Justin Hamilton    |        0.60|
| 288 | MIN  | Arinze Onuaku      |        0.60|
| 289 | MIN  | Adreian Payne      |        0.60|
| 290 | MIN  | Nikola Pekovic     |        0.60|
| 291 | MIN  | Lorenzo Brown      |        0.60|
| 292 | MIN  | Shabazz Muhammad   |        0.60|
| 293 | MIN  | Robbie Hummel      |        0.60|
| 294 | MIN  | Ronny Turiaf       |        0.60|
| 94  | DAL  | Kendrick Perkins   |        0.59|
| 95  | DAL  | J.j. Barea         |        0.59|
| 96  | DAL  | Al-farouq Aminu    |        0.59|
| 97  | DAL  | Chandler Parsons   |        0.59|
| 98  | DAL  | Tyson Chandler     |        0.59|
| 99  | DAL  | Dwight Powell      |        0.59|
| 100 | DAL  | Dirk Nowitzki      |        0.59|
| 101 | DAL  | Devin Harris       |        0.59|
| 102 | DAL  | Bernard James      |        0.59|
| 103 | DAL  | Raymond Felton     |        0.59|
| 104 | DAL  | Monta Ellis        |        0.59|
| 105 | DAL  | Greg Smith         |        0.59|
| 106 | DAL  | Amare Stoudemire   |        0.59|
| 107 | DAL  | Rajon Rondo        |        0.59|
| 108 | DAL  | Charl Villanueva   |        0.59|
| 109 | DAL  | Richar Jefferson   |        0.59|
| 64  | CHI  | E'twaun Moore      |        0.59|
| 65  | CHI  | Taj Gibson         |        0.59|
| 66  | CHI  | Jimmy Butler       |        0.59|
| 67  | CHI  | Joakim Noah        |        0.59|
| 68  | CHI  | Aaron Brooks       |        0.59|
| 69  | CHI  | Nikola Mirotic     |        0.59|
| 70  | CHI  | Nazr Mohammed      |        0.59|
| 71  | CHI  | Mike Dunleavy      |        0.59|
| 72  | CHI  | Pau Gasol          |        0.59|
| 73  | CHI  | Doug Mcdermott     |        0.59|
| 74  | CHI  | Cameron Bairstow   |        0.59|
| 75  | CHI  | Kirk Hinrich       |        0.59|
| 76  | CHI  | Tony Snell         |        0.59|
| 77  | CHI  | Derrick Rose       |        0.59|
| 31  | BRO  | Mason Plumlee      |        0.59|
| 32  | BRO  | Jarrett Jack       |        0.59|
| 33  | BRO  | Brandon Davies     |        0.59|
| 34  | BRO  | Cory Jefferson     |        0.59|
| 35  | BRO  | Mirza Teletovic    |        0.59|
| 36  | BRO  | Darius Morris      |        0.59|
| 37  | BRO  | Joe Johnson        |        0.59|
| 38  | BRO  | Andrei Kirilenko   |        0.59|
| 39  | BRO  | Jerome Jordan      |        0.59|
| 40  | BRO  | Bojan Bogdanovic   |        0.59|
| 41  | BRO  | Deron Williams     |        0.59|
| 42  | BRO  | Alan Anderson      |        0.59|
| 43  | BRO  | Thaddeus Young     |        0.59|
| 44  | BRO  | Sergey Karasev     |        0.59|
| 45  | BRO  | Brook Lopez        |        0.59|
| 46  | BRO  | Markel Brown       |        0.59|
| 47  | BRO  | Earl Clark         |        0.59|
| 171 | IND  | Donald Sloan       |        0.58|
| 172 | IND  | Roy Hibbert        |        0.58|
| 173 | IND  | Paul George        |        0.58|
| 174 | IND  | George Hill        |        0.58|
| 175 | IND  | Damjan Rudez       |        0.58|
| 176 | IND  | Chris Copeland     |        0.58|
| 177 | IND  | David West         |        0.58|
| 178 | IND  | Shay Whittington   |        0.58|
| 179 | IND  | C.j. Miles         |        0.58|
| 180 | IND  | Ian Mahinmi        |        0.58|
| 181 | IND  | Lavoy Allen        |        0.58|
| 182 | IND  | C.j. Watson        |        0.58|
| 183 | IND  | Luis Scola         |        0.58|
| 184 | IND  | Rodney Stuckey     |        0.58|
| 185 | IND  | Solomon Hill       |        0.58|
| 361 | PHI  | Ish Smith          |        0.57|
| 362 | PHI  | Jerami Grant       |        0.57|
| 363 | PHI  | Malcolm Lee        |        0.57|
| 364 | PHI  | Malcolm Thomas     |        0.57|
| 365 | PHI  | Hollis Thompson    |        0.57|
| 366 | PHI  | Robert Covington   |        0.57|
| 367 | PHI  | Tony Wroten        |        0.57|
| 368 | PHI  | Isaiah Canaan      |        0.57|
| 369 | PHI  | Glenn Robinson     |        0.57|
| 370 | PHI  | Thomas Robinson    |        0.57|
| 371 | PHI  | Furkan Aldemir     |        0.57|
| 372 | PHI  | Henry Sims         |        0.57|
| 373 | PHI  | Nerlens Noel       |        0.57|
| 374 | PHI  | Luc Mbah\_a\_moute |        0.57|
| 375 | PHI  | Javale Mcgee       |        0.57|
| 376 | PHI  | Drew Gordon        |        0.57|
| 377 | PHI  | Larry Drew         |        0.57|
| 378 | PHI  | Jakarr Sampson     |        0.57|
| 379 | PHI  | Jason Richardson   |        0.57|
| 346 | ORL  | Tobias Harris      |        0.56|
| 347 | ORL  | Luke Ridnour       |        0.56|
| 348 | ORL  | Willie Green       |        0.56|
| 349 | ORL  | Devyn Marble       |        0.56|
| 350 | ORL  | Aaron Gordon       |        0.56|
| 351 | ORL  | Ben Gordon         |        0.56|
| 352 | ORL  | Victor Oladipo     |        0.56|
| 353 | ORL  | Dewayne Dedmon     |        0.56|
| 354 | ORL  | Nikola Vucevic     |        0.56|
| 355 | ORL  | Kyle O'quinn       |        0.56|
| 356 | ORL  | Maurice Harkless   |        0.56|
| 357 | ORL  | Andrew Nicholson   |        0.56|
| 358 | ORL  | Evan Fournier      |        0.56|
| 359 | ORL  | Channing Frye      |        0.56|
| 360 | ORL  | Elfrid Payton      |        0.56|
| 459 | UTA  | Bryce Cotton       |        0.56|
| 460 | UTA  | Alec Burks         |        0.56|
| 461 | UTA  | Patr Christopher   |        0.56|
| 462 | UTA  | Jerrelle Benimon   |        0.56|
| 463 | UTA  | Rodney Hood        |        0.56|
| 464 | UTA  | Rudy Gobert        |        0.56|
| 465 | UTA  | Derrick Favors     |        0.56|
| 466 | UTA  | Elijah Millsap     |        0.56|
| 467 | UTA  | Joe Ingles         |        0.56|
| 468 | UTA  | Gordon Hayward     |        0.56|
| 469 | UTA  | Jeremy Evans       |        0.56|
| 470 | UTA  | Trey Burke         |        0.56|
| 471 | UTA  | Jack Cooley        |        0.56|
| 472 | UTA  | Trevor Booker      |        0.56|
| 473 | UTA  | Dante Exum         |        0.56|
| 474 | UTA  | Chris Johnson      |        0.56|
| 475 | UTA  | Grant Jerrett      |        0.56|
| 48  | CHA  | Cody Zeller        |        0.55|
| 49  | CHA  | Noah Vonleh        |        0.55|
| 50  | CHA  | Bismack Biyombo    |        0.55|
| 51  | CHA  | Al Jefferson       |        0.55|
| 52  | CHA  | Lance Stephenson   |        0.55|
| 53  | CHA  | Jason Maxiell      |        0.55|
| 54  | CHA  | Troy Daniels       |        0.55|
| 55  | CHA  | Marvin Williams    |        0.55|
| 56  | CHA  | Jeff Taylor        |        0.55|
| 57  | CHA  | Brian Roberts      |        0.55|
| 58  | CHA  | M Kidd-gilchrist   |        0.55|
| 59  | CHA  | Kemba Walker       |        0.55|
| 60  | CHA  | Mo Williams        |        0.55|
| 61  | CHA  | Jannero Pargo      |        0.55|
| 62  | CHA  | Gerald Henderson   |        0.55|
| 63  | CHA  | P.j. Hairston      |        0.55|
| 125 | DET  | Caron Butler       |        0.54|
| 126 | DET  | Spence Dinwiddie   |        0.54|
| 127 | DET  | Joel Anthony       |        0.54|
| 128 | DET  | Cartier Martin     |        0.54|
| 129 | DET  | Ke Caldwell-pope   |        0.54|
| 130 | DET  | Jodie Meeks        |        0.54|
| 131 | DET  | Anthony Tolliver   |        0.54|
| 132 | DET  | Greg Monroe        |        0.54|
| 133 | DET  | Brandon Jennings   |        0.54|
| 134 | DET  | Reggie Jackson     |        0.54|
| 135 | DET  | Andre Drummond     |        0.54|
| 136 | DET  | Shawne Williams    |        0.54|
| 137 | DET  | Tayshaun Prince    |        0.54|
| 138 | DET  | Quincy Miller      |        0.54|
| 139 | DET  | John Lucas         |        0.54|
| 1   | ATL  | Jeff Teague        |        0.52|
| 2   | ATL  | Kyle Korver        |        0.52|
| 3   | ATL  | Thabo Sefolosha    |        0.52|
| 4   | ATL  | Shelvin Mack       |        0.52|
| 5   | ATL  | Elton Brand        |        0.52|
| 6   | ATL  | Al Horford         |        0.52|
| 7   | ATL  | Austin Daye        |        0.52|
| 8   | ATL  | Dennis Schroder    |        0.52|
| 9   | ATL  | Pero Antic         |        0.52|
| 10  | ATL  | Demarre Carroll    |        0.52|
| 11  | ATL  | Kent Bazemore      |        0.52|
| 12  | ATL  | Mike Muscala       |        0.52|
| 13  | ATL  | Mike Scott         |        0.52|
| 14  | ATL  | John Jenkins       |        0.52|
| 15  | ATL  | Paul Millsap       |        0.52|
| 429 | SAN  | Danny Green        |        0.52|
| 430 | SAN  | Kyle Anderson      |        0.52|
| 431 | SAN  | Reggie Williams    |        0.52|
| 432 | SAN  | Tiago Splitter     |        0.52|
| 433 | SAN  | Cory Joseph        |        0.52|
| 434 | SAN  | Kawhi Leonard      |        0.52|
| 435 | SAN  | Tim Duncan         |        0.52|
| 436 | SAN  | Marco Belinelli    |        0.52|
| 437 | SAN  | Matt Bonner        |        0.52|
| 438 | SAN  | Aron Baynes        |        0.52|
| 439 | SAN  | Jeff Ayres         |        0.52|
| 440 | SAN  | Boris Diaw         |        0.52|
| 441 | SAN  | Patty Mills        |        0.52|
| 442 | SAN  | Manu Ginobili      |        0.52|
| 443 | SAN  | Tony Parker        |        0.52|
| 110 | DEN  | J.j. Hickson       |        0.52|
| 111 | DEN  | Ty Lawson          |        0.52|
| 112 | DEN  | Wilson Chandler    |        0.52|
| 113 | DEN  | Jameer Nelson      |        0.52|
| 114 | DEN  | Will Barton        |        0.52|
| 115 | DEN  | Joffre Lauvergne   |        0.52|
| 116 | DEN  | Kenneth Faried     |        0.52|
| 117 | DEN  | Jusuf Nurkic       |        0.52|
| 118 | DEN  | Gary Harris        |        0.52|
| 119 | DEN  | Erick Green        |        0.52|
| 120 | DEN  | Ian Clark          |        0.52|
| 121 | DEN  | Randy Foye         |        0.52|
| 122 | DEN  | Darrell Arthur     |        0.52|
| 123 | DEN  | Jamaal Franklin    |        0.52|
| 124 | DEN  | Danilo Gallinari   |        0.52|
| 258 | MIL  | Khris Middleton    |        0.51|
| 259 | MIL  | O.j. Mayo          |        0.51|
| 260 | MIL  | Kenyon Martin      |        0.51|
| 261 | MIL  | Larry Sanders      |        0.51|
| 262 | MIL  | Jabari Parker      |        0.51|
| 263 | MIL  | Tyler Ennis        |        0.51|
| 264 | MIL  | Jorge Gutierrez    |        0.51|
| 265 | MIL  | Ersan Ilyasova     |        0.51|
| 266 | MIL  | John Henson        |        0.51|
| 267 | MIL  | Jared Dudley       |        0.51|
| 268 | MIL  | Zaza Pachulia      |        0.51|
| 269 | MIL  | G Antetokounmpo    |        0.51|
| 270 | MIL  | Johnny O'bryant    |        0.51|
| 271 | MIL  | Jerryd Bayless     |        0.51|
| 272 | MIL  | Miles Plumlee      |        0.51|
| 273 | MIL  | Carter-williams    |        0.51|
| 274 | MIL  | Kendall Marshall   |        0.51|
| 476 | WAS  | Nene Hilario       |        0.49|
| 477 | WAS  | Drew Gooden        |        0.49|
| 478 | WAS  | Kris Humphries     |        0.49|
| 479 | WAS  | Rasual Butler      |        0.49|
| 480 | WAS  | John Wall          |        0.49|
| 481 | WAS  | Dejuan Blair       |        0.49|
| 482 | WAS  | Will Bynum         |        0.49|
| 483 | WAS  | Martell Webster    |        0.49|
| 484 | WAS  | Glen Rice          |        0.49|
| 485 | WAS  | Otto Porter        |        0.49|
| 486 | WAS  | Kevin Seraphin     |        0.49|
| 487 | WAS  | Ramon Sessions     |        0.49|
| 488 | WAS  | Bradley Beal       |        0.49|
| 489 | WAS  | Paul Pierce        |        0.49|
| 490 | WAS  | Marcin Gortat      |        0.49|
| 491 | WAS  | Toure' Murry       |        0.49|
| 492 | WAS  | Garrett Temple     |        0.49|
