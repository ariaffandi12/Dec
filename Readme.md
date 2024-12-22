#pylint:disable=E0001
import re

from typing import Optional
def function(source: str, function_name: str) -> str:
    pattern: str = r"(" + function_name + r"(?:[\s]+)?\()"
    while True:
        func_names = re.findall(pattern, source)
        if len(func_names) == 0:
            break

        for func_name in func_names:
            index = source.find(func_name)
            if index:
                break

        if index == -1:
            break
        text = func_name
        open_brakets = 1
        for char in source[index + len(func_name):]:
            text += char
            if char == ")":
                open_brakets -= 1
            elif char == "(":
                open_brakets += 1
            if open_brakets == 0:
                break

        yield source[source.find(text):source.find(text) + len(text)]
        source = source[:source.find(text)] + source[source.find(text) + len(text):]
def show_code(source: str, temp):
    if not temp:
        p = Process(target=show_code, args=(source, 1))
        p.start()
        p.join(5)
        if p.is_alive():
            p.kill()
            console.print("# [yellow]can't show the code because the file is too big![/yellow]")
    else:
        syntax = Syntax(source, "python", line_numbers=True)
        console.print(syntax)

class DecompilePyc:
    def __init__(self, filename: str):
        self.filename = filename
        
        self.std = Popen(["pycdc2", filename], stdout=PIPE,
                         stderr=PIPE)

    def get_source(self) -> Optional[str]:
        out = self.std.stdout.read().decode()
        err = self.std.stderr.read().decode()
        if out and err:
            return out + '\n' + err
        elif out:
            return out
        else:
            #print(err)
            return None
import marshal
import base64
import zlib
import os
import time
import dis
R = '\033[1;31m' #احمر
X = '\033[1;33m' #اصفر
F = '\033[2;32m' #اخضر
C = "\033[1;97m" #ابيض
B = '\033[2;36m'#سمائي
Y = '\033[1;34m' #ازرق فاتح.
E = '\033[1;31m'
B = '\033[2;36m'
G = '\033[1;32m'
S = '\033[1;33m'
SA = '\x1b[38;5;216m'
S2A = '\x1b[1;36m'
S3A = '\x1b[38;5;180m'
S4A= '\x1b[38;5;88m' 
S5A = "\x1b[1;32m" 
S6A= '\x1b[38;5;166m'
K = '\033[2;35m'
a1='\x1b[38;5;161m'#وردي جميل جدا
a1 = '\x1b[1;31m'  # أحمر
a2 = '\x1b[1;34m'  # أزرق
a3 = '\x1b[1;32m'  # أخضر
a4 = '\x1b[1;33m'  # أصفر
a5 = '\x1b[38;5;208m'  # برتقالي
a6 = '\x1b[38;5;5m'  # أرجواني
a7 = '\x1b[38;5;13m'  # وردي
a8 = '\x1b[1;30m'  # أسود
a9 = '\x1b[1;37m'  # أبيض
a10 = '\x1b[38;5;52m'  # بني
a11 = '\x1b[38;5;8m'  # رمادي
a12 = '\x1b[38;5;220m'  # ذهبي
a13 = '\x1b[38;5;7m'  # فضي
a14 = '\x1b[38;5;153m'  # أزرق فاتح
a15 = '\x1b[38;5;18m'  # أزرق داكن
a16 = '\x1b[38;5;48m'  # أخضر فاتح
a17 = '\x1b[38;5;22m'  # أخضر داكن
a18 = '\x1b[38;5;196m'  # أحمر فاتح
a19 = '\x1b[38;5;88m'  # أحمر داكن
a20 = '\x1b[38;5;226m'  # أصفر فاتح
a21 = '\x1b[38;5;136m'  # أصفر داكن
a22 = '\x1b[38;5;216m'  # برتقالي فات
a23 = '\x1b[38;5;166m'  # برتقالي داكن
a24 = '\x1b[38;5;234m'  # أرجواني فاتح
a25 = '\x1b[38;5;91m'  # أرجواني داكن
a26 = '\x1b[38;5;205m'  # وردي فاتح
a27 = '\x1b[38;5;161m'  # وردي داكن
a28 = '\x1b[38;5;236m'  # أسود فاتح
a29 = '\x1b[38;5;233m'  # أسود داكن
a30 = '\x1b[38;5;255m'  # أبيض فاتح
a31 = '\x1b[38;5;231m'  # أبيض داكن
a32 = '\x1b[38;5;180m'  # بني فاتح
a33 = '\x1b[38;5;94m'  # بني داكن
a34 = '\x1b[38;5;252m'  # رمادي فاتح
a35 = '\x1b[38;5;246m'  # رمادي داكن
a36 = '\x1b[38;5;228m'  # ذهبي فاتح
a37 = '\x1b[38;5;172m'  # ذهبي داكن
a38 = '\x1b[38;5;188m'  # فضي فاتح
a39 = '\x1b[38;5;247m'  # فضي داكن
a40 = '\x1b[38;5;117m'  # أزرق سماوي
R = '\033[1;31m' #احمر
X = '\033[1;33m' #اصفر
F = '\033[2;32m' #اخضر
C = "\033[1;97m" #ابيض
B = '\033[2;36m'#سمائي
W = '\033[1;34m' #ازرق فاتح.
E = '\033[1;31m'
B = '\033[2;36m'
G = '\033[1;32m'
S = '\033[1;33m'
Z = '\033[1;31m' 
F = '\033[2;32m'
G2 = '\x1b[1;32m'
G1 = '\x1b[1;97m'
G2 = '\x1b[38;5;196m'
G3 = '\x1b[1;33m'
G4 = '\x1b[1;96m'
G5 = '\x1b[38;5;8m'
G6 = '\x1b[38;5;48m'
G7 = '\x1b[38;5;47m'
G8 = '\x1b[38;5;49m'
G9 = '\x1b[38;5;50m'
G10 = '\x1b[1;34m'
G11 = '\x1b[38;5;14m'
G12 = '\x1b[38;5;123m'
G13 = '\x1b[38;5;122m'
G14 = '\x1b[38;5;86m'
G14 = '\x1b[38;5;121m'
G15 = '\x1b[38;5;205m'
G16 = '\x1b[1;92m\x1b[38;5;208m'
G17 = '\x1b[1;92m\x1b[38;5;209m'
G18 = '\x1b[1;92m\x1b[38;5;210m'
G19 = '\x1b[1;92m\x1b[38;5;211m'
G20 = '\x1b[1;92m\x1b[38;5;212m'
G21 = '\x1b[1;92m\x1b[38;5;46m'
G23 = '\x1b[1;92m\x1b[38;5;47m'
G24 = '\x1b[1;92m\x1b[38;5;48m'
G25 = '\x1b[1;92m\x1b[38;5;49m'
G26 = '\x1b[1;92m\x1b[38;5;50m'
os.system("clear")




 
   
 
def decode():
    
  #      print('')
 #    elif choice == "2":
    print('')
    print('\x1b[1;92m\x1b[38;5;221m〖01〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;48m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;208mmarshal Use_marshal_magic ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;222m〖02〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;49m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;209m Lambda  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;223m〖03〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;47m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;210m base64 zlib  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;224m〖04〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;50m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;211m Uncompyle6  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;225m〖05〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;46m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;212m Mardis  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;226m〖06〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;45m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;213m pycdc  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;227m〖07〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;44m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;214m Strings  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;228m〖08〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;43m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;207m marshal magic  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;229m〖09〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;42m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;206m  lock 🔒  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;230m〖10〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;41m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;215m  Lambda Marshal - Base64 - Zlib ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;231m〖11〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;40m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;232m  Lambda Marshal - Base64 - base85 ')   
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;272m〖12〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;39m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;216m Emoji  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;273m〖13〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;38m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;205m Lambda zlib  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;274m〖14〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;37m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;217m Lambad base64  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;275m〖15〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;36m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;218m marshal3.9  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;276m〖16〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;35m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;219m marshal Many types   ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;277m〖17〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;34m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;220m HEX  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;278m〖18〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;33m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;204m codecs  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;279m〖19〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;32m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;203m base64  ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;280m〖20〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;31m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;202m Lambad marshal base64 zlib  ')

    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;280m〖21〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;01m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;201m Lambad marshal base64 zlib lzma gzip ')
    print('\033[0m    ▭▬▭▬▭▬         ▭▬▭▬▭▬          ')
    print('\x1b[1;92m\x1b[38;5;280m〖22〗--»\033[1;34m  \x1b[1;92m\x1b[38;5;01m⌯╼═══❬Decode═══╾⌯\x1b[0;34m\x1b[1;97m ➤ \x1b[1;92m\x1b[38;5;201m Lambad marshal base64 zlib lzma gzip √ DECODE BOT ')

    
    
    print('')    
    while True:
        choice = input("\033[1;97m[√] - Choose : ")
        if choice == "1":      
            
            os.system("clear")
            print('')          
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m - Enter File : ")
            data=str(open(file,"r").read())
            open("Dec_Devil.py","w").write(data)
            os.system(f'marshal-magic Dec_Devil.py -m normal -o  Decode_Dev.py')                    
            print('')
            time.sleep(2)
            print('\n') 
            print('[•] Decode Done √')
            time.sleep(1)
            exit()
        elif choice == "2":
            os.system("clear")
            alose2()
            print("")
        elif choice == "3":
            os.system("clear")
            alose3()
            print('')
        elif choice == "4":
            os.system("clear")
            alose4()
            print('')
        elif choice == "5":
            os.system("clear")
            alose5()
            print('')
        elif choice == "6":
            os.system("clear")
            alose6()
            print("")
        elif choice == "7":
            os.system("clear")
            alose7()
            print('')            
        elif choice == "8":
            os.system("clear")
            alose8()
            print('')
        elif choice == "9":
            os.system("clear")
            alose9()
            print('')
        elif choice == "10":
            os.system("clear")
            alose10()
            print('')
        elif choice == "11":
            os.system("clear")
            alose11()
            print('')
        elif choice == "12":
            os.system("clear")
            alose12()
            print('')
        elif choice == "13":
            os.system("clear")
            alose13()
            print('')
        elif choice == "14":
            os.system("clear")
            alose14()
            print('')
        elif choice == "15":
              os.system("clear")
              os.system("python3.9 /storage/emulated/0/FIX_KEY/AMER")
        elif choice == "16":
              os.system("clear")
              os.system("python3.9 /storage/emulated/0/FIX_KEY/AMER")
        elif choice == "17":
            os.system("clear")
            alose17()
        elif choice == "18":
            os.system("clear")
            alose18()
        elif choice == "19":
            os.system("clear")
            alose19()            
        elif choice == "20":
            os.system("clear")
            alose20()
        elif choice == "21":
            os.system("clear")
            alose21()
        elif choice == "22":
              os.system("clear")
              os.system("python3.9 /storage/emulated/0/FIX_KEY/AMER")    
def alose2():
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            open("Dec_Als.py","w").write(data)
            os.system("python2 Dec_Als.py > Decode_Dec_Als.py")
            print('')                                  
            time.sleep(2)
            print('[•] Decode Done √')
            time.sleep(1)
            exit()  
            
def alose2():
            os.system("clear")
            print('')
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            open("Als_By.py","w").write(data)
            os.system("python2 Als_By.py > Decode_Als_By.py")
            print('')                                  
            time.sleep(2)
            print('[•] Decode Done √')
            time.sleep(1)
            exit()   
def alose3():
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","encrypt1 = ")
            data2=f"""{data}\nwith open('dec_file.py','w') as file: 
            file.write(str(encrypt1))"""
            
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Dec_Als.py")
            print('')                                  
            time.sleep(2)
            print('[•] Decode Done √')
            time.sleep(1)
            exit()	                 
        
def alose4():     
            os.system("clear")
            print('Welcome To Decode Uncompyle 6 [Under Maintenance]')
            print('')          
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")         
            data=str(open(file,"r").read())
            open("Als_By.py","w").write(data)
            os.system(f'marshal-magic Als_By.py -m normal -o Decode_Als_By.py')                    
            alose=str(open("Decode_Als_By.py","r").read())
            data3=f"""#Decode By "Als_By"\n{alose}"""
            open("Decode_Als_By.py","w").write(data3)
            time.sleep(1)
            print('\n') 
            print('[•] Decode Done √')
            time.sleep(1)
            os.system("clear")
            exit()   
def alose5():
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            with open(file, mode='w') as save_dis:
                os.system(f'mardis {file}')
            exit()           
            print('')
            time.sleep(2)
            print('\n') 
            print('[•] Decode Done √')
            time.sleep(1)
            exit() 
            
def alose6():    
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")       
            with open(file, mode='w') as save_dis:
                os.system(f'pycdc {file}')
                time.sleep(2)
                print('\n')
                print('[•] Decode Done √')    
                time.sleep(1)
                exit()
                
def alose7():    
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")         
            with open(file, mode='w') as save_dis:
                os.system(f'strings {file}')
                time.sleep(2)
                print('\n')
                print('[•] Decode Done √')    
                time.sleep(1)
                exit()
def alose8():    
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")         
            data=str(open(file,"r").read())
            open("Als_By.py","w").write(data)
            os.system(f'marshal-magic Als_By.py -m normal -o Decode_Als_By.py')                    
            print('')
            time.sleep(2)
            print('\n') 
            print('[•] Decode Done √')
            time.sleep(1)
            exit()

def alose9():    
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec(marshal.loads(zlib.decompress(base64.b64decode(code.encode()))))","print((zlib.decompress(base64.b64decode(code.encode()))))")
            open("Dec_Als.py","w").write(data)
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            print('')
            time.sleep(2)
            print('\n') 
            print('[•] Decode Done √')
            time.sleep(1)
            exit()            
def alose10():                          
            os.system("clear")
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("_ = lambda __ : __import__('marshal').loads(__import__('zlib').decompress(__import__('base64').b64decode(__[::-1])));exec((_)(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -v 3.9 -o Decode_Dec_Als.py")
            print('')
            print('\n') 
            print('[•] Decode Done √')
            alose10()
def alose11():    
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")  
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")             
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")                         
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("exec(_(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""#Decode By Dec\nimport marshal\nexec(marshal.loads({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -m normal -o Decode_Dec_Als.py")                                     
            print('')
            print('\n') 
            print('[•] Decode Done √')
            exit()     
def alose12():    
            print('')
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            open("Als_By.py","w").write(data)
            os.system("python Als_By.py > Decode_Als_By.py")
            alose=str(open("Decode_Als_By.py","r").read())
            data3=f"""#Decode By "Als"\n{alose}"""
            open("Decode_Als_By.py","w").write(data3)    
            alose2()    
def alose13():    
            print('Decode |  lambad zlib')
            print('')
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            data2="""_ = lambda __ : __import__('zlib').decompress(__[::-1])\n"""
            open("Dec_Als.py","w").write(data)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
   
            print('[•] Decode gone √')
            time.sleep(1)
            print('')
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
 
            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
       
            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
 
            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
       
            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
 
            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
       
            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            time.sleep(1)
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
 
            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
       
            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
          
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
 
            print('[•] Decode gone √')
   
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
          
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  

            print('[•] Decode gone √')
            
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            
            data2=f"""_ = lambda __ : __import__('zlib').decompress(__[::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            print('')                                  
       
            print('[•] Decode gone √')
            exit()

def alose14():    
            
            print('')        
            file=input("\033[2;32m[\x1b[\x1b[38;5;208mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")            
            data2=f"""_ = lambda  : import('base64').b64decode([::-1]);{data}"""
            open("Dec_Als.py","w").write(data2)
            os.system("python2 Dec_Als.py > Decode_Als_By.py")
            als=str(open("Decode_Als_By.py","r").read())
            data3=f"""#Decode By "Dec als"\n{als}"""
            open("Decode_Als_By.py","w").write(data3)   
def alose15():
            print('')        
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")            
            data2=f"""_ = lambda __ : __import__('base64').b64decode(__[::-1]);{data}"""
            open("Als_By.py","w").write(data2)
            os.system("python2 Als_By.py > Decode_Als_By.py")
            als=str(open("Decode_Als_By.py","r").read())
            data3=f"""#Decode By "Dec als"\n{als}"""
            open("Decode_Als_By.py","w").write(data3)
            alose15()
def alose17():
            print('')
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            open("Als_By.py","w").write(data)
            os.system("python Als_By.py > Decode_Als_By.py")
            alose=str(open("Decode_Als_By.py","r").read())
            data3=f"""#Decode By "Als"\n{alose}"""
            open("Decode_Als_By.py","w").write(data3)    
            alose17()    
def alose18():
            print('')
            file=input("\x1b[1;31m[\x1b[1;31mAls\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            open("dec_codecs.py","w").write(data)
            os.system("python dec_codecs.py > Decode_Als_codecs.py")
            alose=str(open("Decode_Als_codecs.py","r").read())
            data3=f"""#Decode By "Als"\n{alose}"""
            open("Decode_Als_codecs.py","w").write(data3)    
            alose18()
def alose19():
            print('')
            file=input("\x1b[1;31m[\x1b[1;31mDec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())
            data=ogge.replace("exec","print")
            open("Als_By.py","w").write(data)
            os.system("python Als_By.py > Decode_Als_By.py")
            alose=str(open("Decode_Als_By.py","r").read())
            data3=f"""#Decode By "Als"\n{alose}"""
            open("Decode_Als_By.py","w").write(data3)   
def alose20():
            os.system("clear")
            file=input("\x1b[1;31m[\x1b[1;31mDecode Plya_Team\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("_ = lambda __ : __import__('marshal').loads(__import__('zlib').decompress(__import__('base64').b64decode(__[::-1])));exec((_)(b","_ =") 
            data2=f"""import base64\nimport zlib\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Plya_Als.py","w").write(data2)            
            os.system("python als_by.py > Decode_Plya_Team.py")
            besto=str(open("Decode_Dec_by.py","r").read())
            data3=f"""#Decode By Plya Team\nimport marshal\nexec(marshal.loads({besto}))"""
            open("Als_by.py","w").write(data3)
            os.system("marshal-magic Plya_Team.py -m normal -o Decode_Plya_Team.py")
            print('')
            print('\n') 
            print('[•] Decode Done √')
            
            
        
            	      	    	      
        

def alose21():                          
            os.system("clear")
            file=input("\x1b[1;31m[\x1b[1;31mDecode Dec\x1b[1;31m] \033[1;97m> Enter File : ")
            ogge=str(open(file,"r").read())          
            data=ogge.replace("_ = lambda __ : __import__('marshal').loads(__import__('gzip').decompress(__import__('lzma').decompress(__import__('zlib').decompress(__import__('base64').b64decode(__[::-1])))));exec((_)(b","_ =") 
            data2=f"""import base64\nimport zlib\nimport lzma\nimport marshal\n{data}\n
y = _[::-1]

d = base64.b64decode(y)

b = zlib.decompress(d)

print(b)
 """           
            open("Dec_Als.py","w").write(data2)            
            os.system("python Dec_Als.py > Decode_Dec_Als.py")
            als=str(open("Decode_Dec_Als.py","r").read())
            data3=f"""_ = lambda __ : __import__('marshal').loads(__import__('gzip').decompress(__import__('lzma').decompress(__import__('zlib').decompress(__import__('base64').b64decode(__[::-1])))));exec((_)({als}))"""
            open("Dec_Als.py","w").write(data3)
            os.system("marshal-magic Dec_Als.py -v 3.9 -m normal -o Decode_Dec_Als.py")
            print('')
            print('\n') 
            print('[•] Decode Done √')
            exit()

                   
                  
                  	           	                  	            	           	                  	            
if __name__ == "__main__":
    decode()