[di+6F26h] = coins
[di+6F22h] = lives

seg000 = 01ed
seg002 = 09c6

bp 01ed:3659 -> run actual game first call


bp 09c6:094C -> run actual game begin func

bp 09c6:0F19


bp 09c6:1048


seg002:032D mov     di, offset aTotalScore ; "TOTAL SCORE:"

bp 01ed:307f 

bp 09c6:0557 getasciicode
bp 09c6:0610  add 10000

bp 09c6:0E30


ds 28af+6f22 == lives

bp 09c6:0497 




for changing time of star ![image](https://github.com/user-attachments/assets/29a059e9-8270-4f88-ae2f-5c46188298c1)


for cheatcheet press `p` then `tab` and enter the letters
```pascal
  EndPause := FALSE;
      Cheat := '';
      While Key = kbP do ;
      While Chr (bKey - $80) = kbP do ;
      OldKey := Key;
      if Key = kbTab then
      begin
        repeat
          if Key <> OldKey then
          begin
            Ch := GetAsciiCode (Key);
            if Key < #$80 then
            begin
              Cheat := Cheat + Key;
              EndPause := (Ch = #0);
            end;
            OldKey := Key;

            if (Cheat = kbT+kbE+kbS+kbT) or    { TEST }
               (Cheat = kb0+kb0+kb4+kb4) then  { 0044 - ShowRetrace }
            begin
              ShowRetrace := not ShowRetrace;
              EndPause := TRUE;
            end;
            if Cheat = kb0+kb3+kbE+kb8 then   { 03E8 - AddLife }
            begin
              AddLife;
              EndPause := TRUE;
            end;
            if Cheat = kbB+kb1+kb7+kb2 then   { B172 - 10000 Lives }
            begin
              Data.Lives[Player] := 10000;
              EndPause := TRUE; 
            end;
            if Cheat = kb9+kbC+kb3+kb2 then    { 9C32 - Star }
            begin
              cdStar := 1;
              EndPause := TRUE;
            end;
            if Cheat = kbF+kb1+kbF+kb2 then    { 9C32 - Champ }
            begin
              cdChamp := 1;
              EndPause := TRUE;
            end;
            if Cheat = kbF+kbF+kbB+kb5 then    { FFB5 - Flower }
            begin
              cdFlower := 1;
              EndPause := TRUE;
            end;
            if Cheat = kbD+kb2+kb3+kb5 then   { D235 - Turbo mode }
            begin
              Turbo := not Turbo;
              EndPause := TRUE;
            end;
            if Cheat = kb7+kb6+kbD+kbD then   { 76DD - Record demo }
            begin
              RecordMacro;
              EndPause := TRUE;
            end;
            if Cheat = kbC+kb7+kbB+kb4 then   { C7B4 - Play demo }
            begin
              PlayMacro;
              EndPause := TRUE;
            end;
            if Cheat = kb2+kb0+kb8+kbD then   { 208D - Save demo (file: $.) }
            begin
              SaveMacro;
              EndPause := TRUE;
            end;

            if Cheat = kb1+kbU+kbP then   { 1UP }
            begin
            { AddLife; }
              if CheatsUsed and 1 = 0 then
              begin
                NewEnemy (tpLife, 0, XView div W, -1, 2, 0, 2);
                CheatsUsed := CheatsUsed or 1;
              end
              else
              begin
                NewEnemy (tpChamp, 1, (XView + Random (100)) div W,
                  -1, 2 - Random (2), 0, 2);
                if Random (10) = 0 then
                  CheatsUsed := CheatsUsed and not 1;
              end;
              EndPause := TRUE;
            end;
            if Cheat = kb2+kb3+kb0+kb5 then   { 2305 - next level }
            begin
              Passed := TRUE;
              Waiting := TRUE;
              TextCounter := 200;
              PipeCode [1] := '�';
              InPipe := TRUE;
              EndPause := TRUE;
            end;
            if Cheat = kbM+kbO+kbN+kbO then  { MONO }
            begin
              PaletteEffect := peBlackWhite;
              RefreshPalette (Palette);
              EndPause := TRUE;
            end;
            if (Cheat = kbE+kbG+kbA+kbM+kbO+kbD+kbE) then  { VGAMODE }
            begin
              PaletteEffect := peEGAMode;
              RefreshPalette (Palette);
              EndPause := TRUE;
            end;
            if (Cheat = kbV+kbG+kbA+kbM+kbO+kbD+kbE) or  { VGAMODE }
               (Cheat = kbC+kbO+kbL+kbO+kbR) then  { COLOR }
            begin
              PaletteEffect := peNoEffect;
              RefreshPalette (Palette);
              EndPause := TRUE;
            end;

            if (Cheat = kbC+kbR+kbE+kbD+kbI+kbT+kbS) then
            begin
              P := @CREDIT;
              Move (P^, PauseText, SizeOf (PauseText));
              for i := 1 to CRED_LEN do
                PauseText[i] := Chr ((Ord (PauseText[i]) - i) - $10 - (((i - 1) mod 8) shl 4));
              if PauseBack <> 0 then
                PopBackGr (PauseBack);
              PauseBack := PushBackGr (XView + 20, 85, 280, 10);
              CenterText (85, PauseText, $0F);
            end;
          end;
        until EndPause;
      end;
```
