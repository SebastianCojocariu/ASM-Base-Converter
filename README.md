Sebastian Cojocariu 321CB UPB ACS                                         
 
	                                		Conversie a unor numere intr-o baza 
					                      aleatorie intre 2 si 16

	Ideea de baza consta in a creea un for in care o sa "mapam" toate 
perechile (nums_array[i],base_array[i]) pentru a putea face convertirea ceruta.
Acest for are drept contor registrul ecx,care initial va fi 0.

for:
    Vom retine in cadrul acestui for ,nums_array[i] in registrul eax.
    Printr-un cmp comparam baza( dword[base_array+4*ecx]) cu 16,respectiv cu 2,pentru a ne asigura ca este intre 2 si 16.
   
   i) Daca baza nu este conform cerintelor de mai sus(intre 2 si 16) facem jmp la label-ul print_mesaj.Aici se va afisa mesajul "Baza incorecta",urmat de incrementarea lui ecx(pentru a se trece la urmatoarea pereche (input,baza)) si compararea acestuia cu valoarea din dword[nums],pentru a ne asigura ca mai avem perechi de verificat:
   1)Daca ecx e mai mic ca valoarea dword[nums] se face jump la label-ul newline care va apela functia NEWLINE de unde se va face un salt neconditionat la for.
   2)In caz contrar se face jump la label-ul final,care incheie CMAIN-ul.
   

   ii)Daca baza este intre 2 si 16 continuam procesul de convertire a inputului in baza ceruta.In registrul ebx vom tine minte numarul de resturi de la impartirea repetata a lui eax la baza,motiv pentru care il initializam cu 0.Cu ajutorul label-ului while_introducere_in_stiva simulam impartirea lui eax la baza cat timp eax!=0,introducand in stiva resturile corespunzatoare si incrementand ebx la fiecare pas(la sfarsitul acestui while ebx va contine numarul de resturi).
      Cu label-ul for_scoatere_din_stiva simulam "scoaterea" resturilor de pe stiva(in registrul eax).In functie de pozitia restului scos fata de 10,facem jump la labelurile corespunzatoare(print_cifra cand eax<=9,respectiv print_char cand eax>=10).Fiecare label transforma numarul primit in reprezentarea din baza data dupa care se face revenirea la label-ul revenire_print.Se decrementeaza ebx,iar daca acesta nu e 0 inseamna ca mai avem resturi de scos din stiva,motiv pentru care facem jump la for_scoatere_din_stiva
     Cand ebx e 0 inseamna ca am scos toate resturile din stiva,deci incrementam ecx(pentru a trece la urmatoarea pereche(input,baza)) si comparam cu dword[nums].Daca ecx e mai mic ca dword[nums] inseamna ca mai avem sigur o pereche (input,baza) dupa aceasta curenta,deci facem jump la label-ul newline pentru a lasa un rand liber(in caz contrar inseamna ca am terminat de parcurs cei 2 vectori si se ajunge in ret,deci CMAIN se incheie).De aici se va face jump la for si se va relua intregul proces de mai sus.

               
