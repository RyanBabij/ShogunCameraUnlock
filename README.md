# Shogun Camera Height Unlock
Unlock the camera height for Shogun Total War

Here are the memory addresses to unlock the camera for Shogun Total War, so you can go lower down and further up. This is for the Steam version.

00DD78E0, 00DD78DC - Camera upper height limit. 2 byte signed. Default value -1000. Set to something like -2000 for higher camera limit.
00A85A68, 00A85A54 - Camera lower height limit. 2 byte signed. Default value -500. Set to something like -100 to go closer to the ground.

Some other stuff I found:

00D93698 - Byte - Keybind for camera up (106 / numpad *)\
00B7D2D4 - 4 bytes unsigned. Camera tilt. 0 = Horizon.\
00B7D2D8 - 4 bytes unsigned. Camera rotation.\
00B7D2C8, 00B7D2CC - 4 bytes unsigned. Camera positions x,y.

I might also see if I can unlock the up/down tilt a little bit. I am hoping to do the same for Medieval Total War in the future.

Here's the relevant section of assembly code, from 0047BA50 to 0047BF28.

```
ShogunM.exe+7BA4F - 90                    - nop 
ShogunM.exe+7BA50 - 53                    - push ebx
ShogunM.exe+7BA51 - 8B DC                 - mov ebx,esp
ShogunM.exe+7BA53 - 83 E4 F8              - and esp,-08 { 248 }
ShogunM.exe+7BA56 - 83 EC 08              - sub esp,08 { 8 }
ShogunM.exe+7BA59 - 55                    - push ebp
ShogunM.exe+7BA5A - 55                    - push ebp
ShogunM.exe+7BA5B - 8B 6B 04              - mov ebp,[ebx+04]
ShogunM.exe+7BA5E - 89 6C 24 04           - mov [esp+04],ebp
ShogunM.exe+7BA62 - 8B EC                 - mov ebp,esp
ShogunM.exe+7BA64 - 81 EC D8000000        - sub esp,000000D8 { 216 }
ShogunM.exe+7BA6A - 89 7D F4              - mov [ebp-0C],edi
ShogunM.exe+7BA6D - 89 75 F0              - mov [ebp-10],esi
ShogunM.exe+7BA70 - A0 8CD2B700           - mov al,[ShogunM.exe+77D28C] { (1) }
ShogunM.exe+7BA75 - A8 01                 - test al,01 { 1 }
ShogunM.exe+7BA77 - 75 11                 - jne ShogunM.exe+7BA8A
ShogunM.exe+7BA79 - 0C 01                 - or al,01 { 1 }
ShogunM.exe+7BA7B - A2 8CD2B700           - mov [ShogunM.exe+77D28C],al { (1) }
ShogunM.exe+7BA80 - B9 90D2B700           - mov ecx,ShogunM.exe+77D290 { (20981) }
ShogunM.exe+7BA85 - E8 96070000           - call ShogunM.exe+7C220
ShogunM.exe+7BA8A - A1 4079DD00           - mov eax,[ShogunM.exe+9D7940] { (0) }
ShogunM.exe+7BA8F - 85 C0                 - test eax,eax
ShogunM.exe+7BA91 - 74 20                 - je ShogunM.exe+7BAB3
ShogunM.exe+7BA93 - B9 C8D2B700           - mov ecx,ShogunM.exe+77D2C8 { (20981) }
ShogunM.exe+7BA98 - E8 83080000           - call ShogunM.exe+7C320
ShogunM.exe+7BA9D - A1 3C5AA800           - mov eax,[ShogunM.exe+685A3C] { (20981) }
ShogunM.exe+7BAA2 - 8B 0D EC78DD00        - mov ecx,[ShogunM.exe+9D78EC] { (35959) }
ShogunM.exe+7BAA8 - 8B 15 405AA800        - mov edx,[ShogunM.exe+685A40] { (-5000) }
ShogunM.exe+7BAAE - E9 7D030000           - jmp ShogunM.exe+7BE30
ShogunM.exe+7BAB3 - 8B 35 D0CAB700        - mov esi,[ShogunM.exe+77CAD0] { (0) }
ShogunM.exe+7BAB9 - 83 FE 05              - cmp esi,05 { 5 }
ShogunM.exe+7BABC - 73 07                 - jae ShogunM.exe+7BAC5
ShogunM.exe+7BABE - BE 05000000           - mov esi,00000005 { 5 }
ShogunM.exe+7BAC3 - EB 0A                 - jmp ShogunM.exe+7BACF
ShogunM.exe+7BAC5 - 83 FE 64              - cmp esi,64 { 100 }
ShogunM.exe+7BAC8 - 76 05                 - jna ShogunM.exe+7BACF
ShogunM.exe+7BACA - BE 64000000           - mov esi,00000064 { 100 }
ShogunM.exe+7BACF - DD 05 A864EF00        - fld qword ptr [ShogunM.exe+AF64A8] { (3.00) }
ShogunM.exe+7BAD5 - D8 0D B0D2B700        - fmul dword ptr [ShogunM.exe+77D2B0] { (1.00) }
ShogunM.exe+7BADB - DD 9D 30FFFFFF        - fstp qword ptr [ebp-000000D0]
ShogunM.exe+7BAE1 - 50                    - push eax
ShogunM.exe+7BAE2 - DD 85 30FFFFFF        - fld qword ptr [ebp-000000D0]
ShogunM.exe+7BAE8 - DB 1C 24              - fistp dword ptr [esp]
ShogunM.exe+7BAEB - 58                    - pop eax
ShogunM.exe+7BAEC - 8B D0                 - mov edx,eax
ShogunM.exe+7BAEE - DD 05 A864EF00        - fld qword ptr [ShogunM.exe+AF64A8] { (3.00) }
ShogunM.exe+7BAF4 - D8 0D B0D2B700        - fmul dword ptr [ShogunM.exe+77D2B0] { (1.00) }
ShogunM.exe+7BAFA - DD 9D 38FFFFFF        - fstp qword ptr [ebp-000000C8]
ShogunM.exe+7BB00 - 50                    - push eax
ShogunM.exe+7BB01 - DD 85 38FFFFFF        - fld qword ptr [ebp-000000C8]
ShogunM.exe+7BB07 - DB 1C 24              - fistp dword ptr [esp]
ShogunM.exe+7BB0A - 58                    - pop eax
ShogunM.exe+7BB0B - 89 55 88              - mov [ebp-78],edx
ShogunM.exe+7BB0E - 89 45 8C              - mov [ebp-74],eax
ShogunM.exe+7BB11 - DD 05 A864EF00        - fld qword ptr [ShogunM.exe+AF64A8] { (3.00) }
ShogunM.exe+7BB17 - D8 0D B0D2B700        - fmul dword ptr [ShogunM.exe+77D2B0] { (1.00) }
ShogunM.exe+7BB1D - DD 9D 40FFFFFF        - fstp qword ptr [ebp-000000C0]
ShogunM.exe+7BB23 - 50                    - push eax
ShogunM.exe+7BB24 - DD 85 40FFFFFF        - fld qword ptr [ebp-000000C0]
ShogunM.exe+7BB2A - DB 1C 24              - fistp dword ptr [esp]
ShogunM.exe+7BB2D - 58                    - pop eax
ShogunM.exe+7BB2E - 8B C8                 - mov ecx,eax
ShogunM.exe+7BB30 - 83 C4 F0              - add esp,-10 { 240 }
ShogunM.exe+7BB33 - 8D 54 24 08           - lea edx,[esp+08]
ShogunM.exe+7BB37 - DD 05 A864EF00        - fld qword ptr [ShogunM.exe+AF64A8] { (3.00) }
ShogunM.exe+7BB3D - D8 0D ACD2B700        - fmul dword ptr [ShogunM.exe+77D2AC] { (1.00) }
ShogunM.exe+7BB43 - DD 9D 48FFFFFF        - fstp qword ptr [ebp-000000B8]
ShogunM.exe+7BB49 - 50                    - push eax
ShogunM.exe+7BB4A - DD 85 48FFFFFF        - fld qword ptr [ebp-000000B8]
ShogunM.exe+7BB50 - DB 1C 24              - fistp dword ptr [esp]
ShogunM.exe+7BB53 - 58                    - pop eax
ShogunM.exe+7BB54 - 8B 3D E066EF00        - mov edi,[ShogunM.exe+AF66E0] { (16383) }
ShogunM.exe+7BB5A - 23 C7                 - and eax,edi
ShogunM.exe+7BB5C - 89 02                 - mov [edx],eax
ShogunM.exe+7BB5E - 8D 54 24 0C           - lea edx,[esp+0C]
ShogunM.exe+7BB62 - DD 05 A864EF00        - fld qword ptr [ShogunM.exe+AF64A8] { (3.00) }
ShogunM.exe+7BB68 - D8 0D ACD2B700        - fmul dword ptr [ShogunM.exe+77D2AC] { (1.00) }
ShogunM.exe+7BB6E - DD 9D 50FFFFFF        - fstp qword ptr [ebp-000000B0]
ShogunM.exe+7BB74 - 50                    - push eax
ShogunM.exe+7BB75 - DD 85 50FFFFFF        - fld qword ptr [ebp-000000B0]
ShogunM.exe+7BB7B - DB 1C 24              - fistp dword ptr [esp]
ShogunM.exe+7BB7E - 58                    - pop eax
ShogunM.exe+7BB7F - 8B 3D E066EF00        - mov edi,[ShogunM.exe+AF66E0] { (16383) }
ShogunM.exe+7BB85 - 23 C7                 - and eax,edi
ShogunM.exe+7BB87 - 89 02                 - mov [edx],eax
ShogunM.exe+7BB89 - 8D 45 90              - lea eax,[ebp-70]
ShogunM.exe+7BB8C - 8D 55 88              - lea edx,[ebp-78]
ShogunM.exe+7BB8F - 89 14 24              - mov [esp],edx
ShogunM.exe+7BB92 - 89 4C 24 04           - mov [esp+04],ecx
ShogunM.exe+7BB96 - 8B C8                 - mov ecx,eax
ShogunM.exe+7BB98 - E8 C3060000           - call ShogunM.exe+7C260
ShogunM.exe+7BB9D - 8B 15 805F7200        - mov edx,[ShogunM.exe+325F80] { (0.09) }
ShogunM.exe+7BBA3 - A1 845F7200           - mov eax,[ShogunM.exe+325F84] { (1.43) }
ShogunM.exe+7BBA8 - DD 05 A064EF00        - fld qword ptr [ShogunM.exe+AF64A0] { (0.00) }
ShogunM.exe+7BBAE - 83 C4 F0              - add esp,-10 { 240 }
ShogunM.exe+7BBB1 - 89 14 24              - mov [esp],edx
ShogunM.exe+7BBB4 - 89 44 24 04           - mov [esp+04],eax
ShogunM.exe+7BBB8 - 89 75 D0              - mov [ebp-30],esi
ShogunM.exe+7BBBB - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BBBE - 85 F6                 - test esi,esi
ShogunM.exe+7BBC0 - 7D 06                 - jnl ShogunM.exe+7BBC8
ShogunM.exe+7BBC2 - DC 05 B064EF00        - fadd qword ptr [ShogunM.exe+AF64B0] { (4294967296.00) }
ShogunM.exe+7BBC8 - DEC9                  - fmulp st(1),st(0)
ShogunM.exe+7BBCA - DD 5C 24 08           - fstp qword ptr [esp+08]
ShogunM.exe+7BBCE - E8 8D002800           - call ShogunM.exe+2FBC60
ShogunM.exe+7BBD3 - 83 C4 10              - add esp,10 { 16 }
ShogunM.exe+7BBD6 - DD 05 9864EF00        - fld qword ptr [ShogunM.exe+AF6498] { (1.00) }
ShogunM.exe+7BBDC - DD 55 F8              - fst qword ptr [ebp-08]
ShogunM.exe+7BBDF - DEE1                  - fsubrp st(1),st(0)
ShogunM.exe+7BBE1 - DD 5D E8              - fstp qword ptr [ebp-18]
ShogunM.exe+7BBE4 - A1 5C5AA800           - mov eax,[ShogunM.exe+685A5C] { (5000) }
ShogunM.exe+7BBE9 - 8B 15 C8D2B700        - mov edx,[ShogunM.exe+77D2C8] { (20981) }
ShogunM.exe+7BBEF - 3B C2                 - cmp eax,edx
ShogunM.exe+7BBF1 - 7E 09                 - jle ShogunM.exe+7BBFC
ShogunM.exe+7BBF3 - 8B D0                 - mov edx,eax
ShogunM.exe+7BBF5 - A3 C8D2B700           - mov [ShogunM.exe+77D2C8],eax { (20981) }
ShogunM.exe+7BBFA - EB 10                 - jmp ShogunM.exe+7BC0C
ShogunM.exe+7BBFC - A1 585AA800           - mov eax,[ShogunM.exe+685A58] { (35959) }
ShogunM.exe+7BC01 - 3B D0                 - cmp edx,eax
ShogunM.exe+7BC03 - 7E 07                 - jle ShogunM.exe+7BC0C
ShogunM.exe+7BC05 - 8B D0                 - mov edx,eax
ShogunM.exe+7BC07 - A3 C8D2B700           - mov [ShogunM.exe+77D2C8],eax { (20981) }
ShogunM.exe+7BC0C - 8B 0D 645AA800        - mov ecx,[ShogunM.exe+685A64] { (5000) }
ShogunM.exe+7BC12 - A1 CCD2B700           - mov eax,[ShogunM.exe+77D2CC] { (35959) }
ShogunM.exe+7BC17 - 3B C8                 - cmp ecx,eax
ShogunM.exe+7BC19 - 7E 0A                 - jle ShogunM.exe+7BC25
ShogunM.exe+7BC1B - 8B C1                 - mov eax,ecx
ShogunM.exe+7BC1D - 89 0D CCD2B700        - mov [ShogunM.exe+77D2CC],ecx { (35959) }
ShogunM.exe+7BC23 - EB 12                 - jmp ShogunM.exe+7BC37
ShogunM.exe+7BC25 - 8B 0D 605AA800        - mov ecx,[ShogunM.exe+685A60] { (35959) }
ShogunM.exe+7BC2B - 3B C1                 - cmp eax,ecx
ShogunM.exe+7BC2D - 7E 08                 - jle ShogunM.exe+7BC37
ShogunM.exe+7BC2F - 8B C1                 - mov eax,ecx
ShogunM.exe+7BC31 - 89 0D CCD2B700        - mov [ShogunM.exe+77D2CC],ecx { (35959) }
ShogunM.exe+7BC37 - 8B 0D DC78DD00        - mov ecx,[ShogunM.exe+9D78DC] { (-5000) }
ShogunM.exe+7BC3D - 8B 3D D0D2B700        - mov edi,[ShogunM.exe+77D2D0] { (-5000) }
ShogunM.exe+7BC43 - 3B CF                 - cmp ecx,edi
ShogunM.exe+7BC45 - 7E 0A                 - jle ShogunM.exe+7BC51
ShogunM.exe+7BC47 - 8B F9                 - mov edi,ecx
ShogunM.exe+7BC49 - 89 0D D0D2B700        - mov [ShogunM.exe+77D2D0],ecx { (-5000) }
ShogunM.exe+7BC4F - EB 12                 - jmp ShogunM.exe+7BC63
ShogunM.exe+7BC51 - 8B 0D 685AA800        - mov ecx,[ShogunM.exe+685A68] { (-100) }
ShogunM.exe+7BC57 - 3B F9                 - cmp edi,ecx
ShogunM.exe+7BC59 - 7E 08                 - jle ShogunM.exe+7BC63
ShogunM.exe+7BC5B - 8B F9                 - mov edi,ecx
ShogunM.exe+7BC5D - 89 0D D0D2B700        - mov [ShogunM.exe+77D2D0],ecx { (-5000) }
ShogunM.exe+7BC63 - 8B 0D A8CAB700        - mov ecx,[ShogunM.exe+77CAA8] { (0584BEC0) }
ShogunM.exe+7BC69 - 85 C9                 - test ecx,ecx
ShogunM.exe+7BC6B - 74 3C                 - je ShogunM.exe+7BCA9
ShogunM.exe+7BC6D - 68 C8D2B700           - push ShogunM.exe+77D2C8 { (20981) }
ShogunM.exe+7BC72 - E8 297EFDFF           - call ShogunM.exe+53AA0
ShogunM.exe+7BC77 - A9 FF000000           - test eax,000000FF { 255 }
ShogunM.exe+7BC7C - 74 1A                 - je ShogunM.exe+7BC98
ShogunM.exe+7BC7E - C6 05 84D2B700 00     - mov byte ptr [ShogunM.exe+77D284],00 { (0),0 }
ShogunM.exe+7BC85 - 8B 15 C8D2B700        - mov edx,[ShogunM.exe+77D2C8] { (20981) }
ShogunM.exe+7BC8B - A1 CCD2B700           - mov eax,[ShogunM.exe+77D2CC] { (35959) }
ShogunM.exe+7BC90 - 8B 3D D0D2B700        - mov edi,[ShogunM.exe+77D2D0] { (-5000) }
ShogunM.exe+7BC96 - EB 11                 - jmp ShogunM.exe+7BCA9
ShogunM.exe+7BC98 - 8B 15 C8D2B700        - mov edx,[ShogunM.exe+77D2C8] { (20981) }
ShogunM.exe+7BC9E - A1 CCD2B700           - mov eax,[ShogunM.exe+77D2CC] { (35959) }
ShogunM.exe+7BCA3 - 8B 3D D0D2B700        - mov edi,[ShogunM.exe+77D2D0] { (-5000) }
ShogunM.exe+7BCA9 - 2B 15 3C5AA800        - sub edx,[ShogunM.exe+685A3C] { (20981) }
ShogunM.exe+7BCAF - 89 55 D0              - mov [ebp-30],edx
ShogunM.exe+7BCB2 - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BCB5 - DD 45 E8              - fld qword ptr [ebp-18]
ShogunM.exe+7BCB8 - DCC9                  - fmul st(1),st(0)
ShogunM.exe+7BCBA - D9C9                  - fxch st(1)
ShogunM.exe+7BCBC - DD 9D 58FFFFFF        - fstp qword ptr [ebp-000000A8]
ShogunM.exe+7BCC2 - 2B 05 EC78DD00        - sub eax,[ShogunM.exe+9D78EC] { (35959) }
ShogunM.exe+7BCC8 - 89 45 D0              - mov [ebp-30],eax
ShogunM.exe+7BCCB - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BCCE - D8C9                  - fmul st(0),st(1)
ShogunM.exe+7BCD0 - DD 9D 60FFFFFF        - fstp qword ptr [ebp-000000A0]
ShogunM.exe+7BCD6 - 2B 3D 405AA800        - sub edi,[ShogunM.exe+685A40] { (-5000) }
ShogunM.exe+7BCDC - 89 7D D0              - mov [ebp-30],edi
ShogunM.exe+7BCDF - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BCE2 - DEC9                  - fmulp st(1),st(0)
ShogunM.exe+7BCE4 - DD 9D 68FFFFFF        - fstp qword ptr [ebp-00000098]
ShogunM.exe+7BCEA - A1 D4D2B700           - mov eax,[ShogunM.exe+77D2D4] { (1024) }
ShogunM.exe+7BCEF - 2B 05 E878DD00        - sub eax,[ShogunM.exe+9D78E8] { (1024) }
ShogunM.exe+7BCF5 - 25 FF3F0000           - and eax,00003FFF { 16383 }
ShogunM.exe+7BCFA - 3D 00200000           - cmp eax,00002000 { 8192 }
ShogunM.exe+7BCFF - 7E 05                 - jle ShogunM.exe+7BD06
ShogunM.exe+7BD01 - 05 00C0FFFF           - add eax,FFFFC000 { -16384 }
ShogunM.exe+7BD06 - 89 45 D0              - mov [ebp-30],eax
ShogunM.exe+7BD09 - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BD0C - DC 4D E8              - fmul qword ptr [ebp-18]
ShogunM.exe+7BD0F - DD 9D 70FFFFFF        - fstp qword ptr [ebp-00000090]
ShogunM.exe+7BD15 - A1 D8D2B700           - mov eax,[ShogunM.exe+77D2D8] { (8176) }
ShogunM.exe+7BD1A - 2B 05 E478DD00        - sub eax,[ShogunM.exe+9D78E4] { (8176) }
ShogunM.exe+7BD20 - 25 FF3F0000           - and eax,00003FFF { 16383 }
ShogunM.exe+7BD25 - 3D 00200000           - cmp eax,00002000 { 8192 }
ShogunM.exe+7BD2A - 7E 05                 - jle ShogunM.exe+7BD31
ShogunM.exe+7BD2C - 05 00C0FFFF           - add eax,FFFFC000 { -16384 }
ShogunM.exe+7BD31 - 89 45 D0              - mov [ebp-30],eax
ShogunM.exe+7BD34 - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BD37 - DD 45 E8              - fld qword ptr [ebp-18]
ShogunM.exe+7BD3A - DEC9                  - fmulp st(1),st(0)
ShogunM.exe+7BD3C - DD 9D 78FFFFFF        - fstp qword ptr [ebp-00000088]
ShogunM.exe+7BD42 - 33 FF                 - xor edi,edi
ShogunM.exe+7BD44 - DD 84 FD 58FFFFFF     - fld qword ptr [ebp+edi*8-000000A8]
ShogunM.exe+7BD4B - DC 1D 9064EF00        - fcomp qword ptr [ShogunM.exe+AF6490] { (0.00) }
ShogunM.exe+7BD51 - DFE0                  - fnstsw ax
ShogunM.exe+7BD53 - 9E                    - sahf 
ShogunM.exe+7BD54 - 74 6B                 - je ShogunM.exe+7BDC1
ShogunM.exe+7BD56 - 8D 4D 90              - lea ecx,[ebp-70]
ShogunM.exe+7BD59 - 57                    - push edi
ShogunM.exe+7BD5A - E8 71050000           - call ShogunM.exe+7C2D0
ShogunM.exe+7BD5F - DD 05 9864EF00        - fld qword ptr [ShogunM.exe+AF6498] { (1.00) }
ShogunM.exe+7BD65 - DC B4 FD 58FFFFFF     - fdiv qword ptr [ebp+edi*8-000000A8]
ShogunM.exe+7BD6C - 0FAF C6               - imul eax,esi
ShogunM.exe+7BD6F - 89 45 D0              - mov [ebp-30],eax
ShogunM.exe+7BD72 - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BD75 - 85 C0                 - test eax,eax
ShogunM.exe+7BD77 - 7D 06                 - jnl ShogunM.exe+7BD7F
ShogunM.exe+7BD79 - DC 05 B064EF00        - fadd qword ptr [ShogunM.exe+AF64B0] { (4294967296.00) }
ShogunM.exe+7BD7F - DEC9                  - fmulp st(1),st(0)
ShogunM.exe+7BD81 - D9E1                  - fabs 
ShogunM.exe+7BD83 - DC 5D F8              - fcomp qword ptr [ebp-08]
ShogunM.exe+7BD86 - DFE0                  - fnstsw ax
ShogunM.exe+7BD88 - 9E                    - sahf 
ShogunM.exe+7BD89 - 73 36                 - jae ShogunM.exe+7BDC1
ShogunM.exe+7BD8B - 8D 4D 90              - lea ecx,[ebp-70]
ShogunM.exe+7BD8E - 57                    - push edi
ShogunM.exe+7BD8F - E8 3C050000           - call ShogunM.exe+7C2D0
ShogunM.exe+7BD94 - DD 05 9864EF00        - fld qword ptr [ShogunM.exe+AF6498] { (1.00) }
ShogunM.exe+7BD9A - DC B4 FD 58FFFFFF     - fdiv qword ptr [ebp+edi*8-000000A8]
ShogunM.exe+7BDA1 - DD 5D F8              - fstp qword ptr [ebp-08]
ShogunM.exe+7BDA4 - 0FAF C6               - imul eax,esi
ShogunM.exe+7BDA7 - 89 45 D0              - mov [ebp-30],eax
ShogunM.exe+7BDAA - DB 45 D0              - fild dword ptr [ebp-30]
ShogunM.exe+7BDAD - 85 C0                 - test eax,eax
ShogunM.exe+7BDAF - 7D 06                 - jnl ShogunM.exe+7BDB7
ShogunM.exe+7BDB1 - DC 05 B064EF00        - fadd qword ptr [ShogunM.exe+AF64B0] { (4294967296.00) }
ShogunM.exe+7BDB7 - DD 45 F8              - fld qword ptr [ebp-08]
ShogunM.exe+7BDBA - DEC9                  - fmulp st(1),st(0)
ShogunM.exe+7BDBC - D9E1                  - fabs 
ShogunM.exe+7BDBE - DD 5D F8              - fstp qword ptr [ebp-08]
ShogunM.exe+7BDC1 - 47                    - inc edi
ShogunM.exe+7BDC2 - 83 FF 05              - cmp edi,05 { 5 }
ShogunM.exe+7BDC5 - 0F8C 79FFFFFF         - jl ShogunM.exe+7BD44
ShogunM.exe+7BDCB - BA 00000000           - mov edx,00000000 { 0 }
ShogunM.exe+7BDD0 - DD 45 F8              - fld qword ptr [ebp-08]
ShogunM.exe+7BDD3 - D9C0                  - fld st(0)
ShogunM.exe+7BDD5 - DC 8C D5 58FFFFFF     - fmul qword ptr [ebp+edx*8-000000A8]
ShogunM.exe+7BDDC - DD 5D 80              - fstp qword ptr [ebp-80]
ShogunM.exe+7BDDF - 50                    - push eax
ShogunM.exe+7BDE0 - DD 45 80              - fld qword ptr [ebp-80]
ShogunM.exe+7BDE3 - DB 1C 24              - fistp dword ptr [esp]
ShogunM.exe+7BDE6 - 58                    - pop eax
ShogunM.exe+7BDE7 - 89 44 95 A4           - mov [ebp+edx*4-5C],eax
ShogunM.exe+7BDEB - 42                    - inc edx
ShogunM.exe+7BDEC - 83 FA 05              - cmp edx,05 { 5 }
ShogunM.exe+7BDEF - 7C E2                 - jl ShogunM.exe+7BDD3
ShogunM.exe+7BDF1 - DDD8                  - fstp st(0)
ShogunM.exe+7BDF3 - A1 3C5AA800           - mov eax,[ShogunM.exe+685A3C] { (20981) }
ShogunM.exe+7BDF8 - 03 45 A4              - add eax,[ebp-5C]
ShogunM.exe+7BDFB - A3 3C5AA800           - mov [ShogunM.exe+685A3C],eax { (20981) }
ShogunM.exe+7BE00 - 8B 0D EC78DD00        - mov ecx,[ShogunM.exe+9D78EC] { (35959) }
ShogunM.exe+7BE06 - 03 4D A8              - add ecx,[ebp-58]
ShogunM.exe+7BE09 - 89 0D EC78DD00        - mov [ShogunM.exe+9D78EC],ecx { (35959) }
ShogunM.exe+7BE0F - 8B 15 405AA800        - mov edx,[ShogunM.exe+685A40] { (-5000) }
ShogunM.exe+7BE15 - 03 55 AC              - add edx,[ebp-54]
ShogunM.exe+7BE18 - 89 15 405AA800        - mov [ShogunM.exe+685A40],edx { (-5000) }
ShogunM.exe+7BE1E - 8B 7D B0              - mov edi,[ebp-50]
ShogunM.exe+7BE21 - 01 3D E878DD00        - add [ShogunM.exe+9D78E8],edi { (1024) }
ShogunM.exe+7BE27 - 8B 75 B4              - mov esi,[ebp-4C]
ShogunM.exe+7BE2A - 01 35 E478DD00        - add [ShogunM.exe+9D78E4],esi { (8176) }
ShogunM.exe+7BE30 - 8B 35 485AA800        - mov esi,[ShogunM.exe+685A48] { (1000) }
ShogunM.exe+7BE36 - 3B F0                 - cmp esi,eax
ShogunM.exe+7BE38 - 7E 0A                 - jle ShogunM.exe+7BE44
ShogunM.exe+7BE3A - 8B C6                 - mov eax,esi
ShogunM.exe+7BE3C - 89 35 3C5AA800        - mov [ShogunM.exe+685A3C],esi { (20981) }
ShogunM.exe+7BE42 - EB 12                 - jmp ShogunM.exe+7BE56
ShogunM.exe+7BE44 - 8B 35 445AA800        - mov esi,[ShogunM.exe+685A44] { (35959) }
ShogunM.exe+7BE4A - 3B C6                 - cmp eax,esi
ShogunM.exe+7BE4C - 7E 08                 - jle ShogunM.exe+7BE56
ShogunM.exe+7BE4E - 8B C6                 - mov eax,esi
ShogunM.exe+7BE50 - 89 35 3C5AA800        - mov [ShogunM.exe+685A3C],esi { (20981) }
ShogunM.exe+7BE56 - 8B 35 505AA800        - mov esi,[ShogunM.exe+685A50] { (5000) }
ShogunM.exe+7BE5C - 3B F1                 - cmp esi,ecx
ShogunM.exe+7BE5E - 7E 0A                 - jle ShogunM.exe+7BE6A
ShogunM.exe+7BE60 - 8B CE                 - mov ecx,esi
ShogunM.exe+7BE62 - 89 35 EC78DD00        - mov [ShogunM.exe+9D78EC],esi { (35959) }
ShogunM.exe+7BE68 - EB 12                 - jmp ShogunM.exe+7BE7C
ShogunM.exe+7BE6A - 8B 35 4C5AA800        - mov esi,[ShogunM.exe+685A4C] { (35959) }
ShogunM.exe+7BE70 - 3B CE                 - cmp ecx,esi
ShogunM.exe+7BE72 - 7E 08                 - jle ShogunM.exe+7BE7C
ShogunM.exe+7BE74 - 8B CE                 - mov ecx,esi
ShogunM.exe+7BE76 - 89 35 EC78DD00        - mov [ShogunM.exe+9D78EC],esi { (35959) }
ShogunM.exe+7BE7C - 8B 35 E078DD00        - mov esi,[ShogunM.exe+9D78E0] { (-5000) }
ShogunM.exe+7BE82 - 3B F2                 - cmp esi,edx
ShogunM.exe+7BE84 - 7E 08                 - jle ShogunM.exe+7BE8E
ShogunM.exe+7BE86 - 89 35 405AA800        - mov [ShogunM.exe+685A40],esi { (-5000) }
ShogunM.exe+7BE8C - EB 10                 - jmp ShogunM.exe+7BE9E
ShogunM.exe+7BE8E - 8B 35 545AA800        - mov esi,[ShogunM.exe+685A54] { (-100) }
ShogunM.exe+7BE94 - 3B D6                 - cmp edx,esi
ShogunM.exe+7BE96 - 7E 06                 - jle ShogunM.exe+7BE9E
ShogunM.exe+7BE98 - 89 35 405AA800        - mov [ShogunM.exe+685A40],esi { (-5000) }
ShogunM.exe+7BE9E - 51                    - push ecx
ShogunM.exe+7BE9F - 50                    - push eax
ShogunM.exe+7BEA0 - E8 6B900600           - call ShogunM.exe+E4F10
ShogunM.exe+7BEA5 - 83 C4 08              - add esp,08 { 8 }
ShogunM.exe+7BEA8 - 85 C0                 - test eax,eax
ShogunM.exe+7BEAA - 7E 02                 - jle ShogunM.exe+7BEAE
ShogunM.exe+7BEAC - 33 C0                 - xor eax,eax
ShogunM.exe+7BEAE - 03 05 405AA800        - add eax,[ShogunM.exe+685A40] { (-5000) }
ShogunM.exe+7BEB4 - A3 F078DD00           - mov [ShogunM.exe+9D78F0],eax { (-7479) }
ShogunM.exe+7BEB9 - 8D 4D B8              - lea ecx,[ebp-48]
ShogunM.exe+7BEBC - E8 5F030000           - call ShogunM.exe+7C220
ShogunM.exe+7BEC1 - B9 90D2B700           - mov ecx,ShogunM.exe+77D290 { (20981) }
ShogunM.exe+7BEC6 - 8D 45 B8              - lea eax,[ebp-48]
ShogunM.exe+7BEC9 - 50                    - push eax
ShogunM.exe+7BECA - E8 C1030000           - call ShogunM.exe+7C290
ShogunM.exe+7BECF - A9 FF000000           - test eax,000000FF { 255 }
ShogunM.exe+7BED4 - 74 09                 - je ShogunM.exe+7BEDF
ShogunM.exe+7BED6 - C6 05 80D2B700 00     - mov byte ptr [ShogunM.exe+77D280],00 { (0),0 }
ShogunM.exe+7BEDD - EB 3D                 - jmp ShogunM.exe+7BF1C
ShogunM.exe+7BEDF - C6 05 80D2B700 01     - mov byte ptr [ShogunM.exe+77D280],01 { (0),1 }
ShogunM.exe+7BEE6 - C7 05 0019C200 00000000 - mov [ShogunM.exe+821900],00000000 { (1),0 }
ShogunM.exe+7BEF0 - 8B 7D B8              - mov edi,[ebp-48]
ShogunM.exe+7BEF3 - 89 3D 90D2B700        - mov [ShogunM.exe+77D290],edi { (20981) }
ShogunM.exe+7BEF9 - 8B 75 BC              - mov esi,[ebp-44]
ShogunM.exe+7BEFC - 89 35 94D2B700        - mov [ShogunM.exe+77D294],esi { (35959) }
ShogunM.exe+7BF02 - 8B 4D C0              - mov ecx,[ebp-40]
ShogunM.exe+7BF05 - 89 0D 98D2B700        - mov [ShogunM.exe+77D298],ecx { (-5000) }
ShogunM.exe+7BF0B - 8B 55 C4              - mov edx,[ebp-3C]
ShogunM.exe+7BF0E - 89 15 9CD2B700        - mov [ShogunM.exe+77D29C],edx { (1024) }
ShogunM.exe+7BF14 - 8B 45 C8              - mov eax,[ebp-38]
ShogunM.exe+7BF17 - A3 A0D2B700           - mov [ShogunM.exe+77D2A0],eax { (8176) }
ShogunM.exe+7BF1C - 8B 75 F0              - mov esi,[ebp-10]
ShogunM.exe+7BF1F - 8B 7D F4              - mov edi,[ebp-0C]
ShogunM.exe+7BF22 - 8B E5                 - mov esp,ebp
ShogunM.exe+7BF24 - 5D                    - pop ebp
ShogunM.exe+7BF25 - 8B E3                 - mov esp,ebx
ShogunM.exe+7BF27 - 5B                    - pop ebx
ShogunM.exe+7BF28 - C3                    - ret 
```
