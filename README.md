# Aplikasi-Absensi.asm

.model small
.org 100h
.data   
    prompt db 'Pilih menu absensi <1-5>: $'
    menu1 db '1. masuk kerja' , 0Ah, 0Dh,'$'   
    menu2 db '2. pulang kerja' , 0Ah, 0Dh,'$'
    menu3 db '3. Cuti' , 0Ah, 0Dh,'$'
    menu4 db '4. Sakit' , 0Ah, 0Dh,'$'
    menu5 db '5. Kerja' , 0Ah, 0Dh,'$'

pilihan db 'Pilihan Anda:' , 0Ah, 0Dh,'$'
hasil db  , 0Ah, 0Dh,'Anda memilih absensi:' , 0Ah, 0Dh,' $'
newline db 0Ah, 0Dh, '$'

.code

main:

; Inisialisasi segment data
mov ax, @data
mov ds, ax

; Menampilkan menu absensi
mov ah, 09h
lea dx, menu1
int 21h

lea dx, menu2
int 21h

lea dx, menu3
int 21h

lea dx, menu4
int 21h

lea dx, menu5
int 21h

; Menampilkan prompt untuk memilih absensi
lea dx, prompt
mov ah, 09h
int 21h

; Input pilihan
mov ah, 01h
int 21h
sub al, '0'     ; Convert ASCII ke angka
mov bl, al      ; Menyimpan pilihan ke dalam register bl

; Menampilkan pilihan
lea dx, hasil
mov ah, 09h
int 21h

; Menampilkan hasil berdasarkan pilihan
cmp bl, 1
je menu_masuk_kerja

cmp bl, 2
je menu_pulang_kerja

cmp bl, 3
je menu_cuti

cmp bl, 4
je menu_sakit

cmp bl, 5
je menu_libur

jmp end_program

menu_masuk_kerja:
lea dx, menu1
mov ah, 09h
int 21h
jmp end_program

menu_pulang_kerja:
lea dx, menu2
mov ah, 09h
int 21h
jmp end_program

menu_cuti:
lea dx, menu3
mov ah, 09h
int 21h
jmp end_program

menu_sakit:
lea dx, menu4
mov ah, 09h
int 21h
jmp end_program

menu_libur:
lea dx, menu5
mov ah, 09h
int 21h
jmp end_program

end_program:

; Menampilkan newline (baris baru setelah output)
lea dx, newline
mov ah, 09h
int 21h

; Keluar dari program
mov ah, 4Ch
int 21h

end main
