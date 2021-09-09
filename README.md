DEF SEG = (&HB800)
CLS
PRINT "Loading"
SLEEP 2
CLS
COLOR 3
PRINT " Loading"
SLEEP 1.1
LOCATE 1, 1: COLOR 15: PRINT "  Please wait"
SLEEP 1

FOR s = 15 TO 24: e = 11 * SIN(e / 111): POKE s * 2 - 1, 15
POKE s * 2, 46
NEXT s
SLEEP 2
REM Fortschrittsanzeige
COLOR 8
FOR s = 10 TO 10000: o = o / 2 + 44 * SIN(s / s) + s: NEXT s
CLS
FOR x = 15 TO 60
LOCATE 23, x
PRINT CHR$(176); INT(100 * (x - 15) / (80 - 15)); "%"
SOUND 22222, 18.2 * 1.2 / 8
NEXT

FOR r = 1 TO 20
LOCATE 23 - r, x - 1
PRINT CHR$(176); INT(100 * (r + x - 16) / (80 - 15)); "%"
SOUND 22222, 18.2 * 1.2 / 8
NEXT r

CLS : REM Bildschirm Spielname
FOR x = 1 TO 14
LOCATE x + 3, x: COLOR INT(x / 2) + 2: PRINT "ÛÛÛÛÛÛ"
NEXT x

FOR x = 14 TO 1 STEP -1
LOCATE x + 3, 15 - x: COLOR INT(x / 2) + 2: PRINT "ÛÛÛÛÛÛ"
NEXT x

FOR x = 1 TO 14: REM Buchstabe I
LOCATE x + 3, 25: COLOR INT(x / 2) + 2: PRINT "ÛÛÛ"
NEXT x

FOR x = 1 TO 1: REM unterer Strich vom L
LOCATE x + 16, 28: COLOR INT(x / 2) + 2: PRINT "ÛÛÛÛÛÛ"
NEXT x

FOR x = 1 TO 14: REM Buchstabe I
LOCATE 18 - x, 37: COLOR INT(x / 2) + 2: PRINT "ÛÛÛ"
NEXT x
SLEEP 5
COLOR 7
SCREEN 13
LOCATE 2, 2: PRINT "BEDIENUNG mit der Tastatur"
SLEEP 4
LOCATE 2, 2: PRINT "Û  Û  Û  Û  Û  Û  Û  Û  Û  Û  Û  Û  Û"
LOCATE 24, 1: PRINT "Beenden mit ESC"
y = 80
FOR d = 0 TO 200
FOR x = 0 TO 319 STEP .2: IF INKEY$ = CHR$(27) THEN 100

IF y < 38 THEN SOUND 220, 1: y = y + 5
IF INP(&H60) < 57 THEN t = INP(&H60)
y = y + t / 50 - .3
IF y > 120 THEN SOUND 37, .1: IF INKEY$ = CHR$(27) THEN GOTO 100
CIRCLE (x, y), 14, 0: REM altes Frame l”schen
CIRCLE (x, y), 15, 0: REM altes Frame l”schen
CIRCLE (x, y), 16, 0: REM altes Frame l”schen
IF INKEY$ = CHR$(27) THEN 100
CIRCLE (x - 10, y - 1), 17, 0: REM altes Frame l”schen
CIRCLE (x - 20, y - 2), 18, 0: REM altes Frame l”schen
CIRCLE (x + 10, y + 1), 19, 0: REM altes Frame l”schen
CIRCLE (x + 2, y + 2), 20, 0: REM altes Frame l”schen
CIRCLE (x, y), 13, 3: REM Kreis zeichnen
IF INKEY$ = CHR$(27) THEN 100
NEXT x, d

100 CLS : COLOR 5: LOCATE 6, 17: PRINT "ENDE": SLEEP 5: COLOR 0:
WHILE INKEY$ <> "": WEND: REM Tastaturpuffer leeren sonst
REM                           Tastatureingaben nach Programmende
REM                           auf der Eingabeaufforderung sichtbar

