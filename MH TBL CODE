#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import os
from datetime import datetime

# =========================
# Banner
# =========================
def banner():
    os.system("clear")
    print("""
========================================
 MH PASS TOOL  - Password Awareness Demo
 Educational Use Only
========================================
""")

# =========================
# Franco Converter
# =========================
def to_franco(word):
    mapping = {
        "a":"a","b":"b","c":"c","d":"d","e":"e",
        "f":"f","g":"g","h":"7","i":"i","j":"g",
        "k":"k","l":"l","m":"m","n":"n","o":"o",
        "p":"p","q":"q","r":"r","s":"s","t":"t",
        "u":"u","v":"v","w":"w","x":"x","y":"y","z":"z"
    }
    result=""
    for ch in word.lower():
        result+=mapping.get(ch,ch)
    return result

# =========================
# Password Variants
# =========================
def variants(word):

    word=word.strip()
    if not word:
        return []

    results=set()

    base_forms={
        word.lower(),
        word.upper(),
        word.capitalize(),
        word[::-1],
        to_franco(word)
    }

    # leet
    leet=(word.lower()
    .replace('a','@')
    .replace('o','0')
    .replace('i','1')
    .replace('e','3')
    .replace('s','$')
    .replace('t','7'))
    base_forms.add(leet)

    numbers=["","1","2","3","5","7","9","10","11","12","123","1234","12345","00","99"]
    years=[str(y) for y in range(1990,datetime.now().year+1)]
    symbols=["!","@","_","."]
    arabic=["a","m","s","h","n"]

    for base in base_forms:

        # ارقام
        for n in numbers:
            results.add(base+n)
            results.add(n+base)

        # سنوات
        for y in years:
            results.add(base+y)

        # رموز
        for s in symbols:
            results.add(base+s)
            results.add(s+base)
            results.add(base+s+"123")

        # تكرار
        results.add(base+base)
        results.add(base+"_"+base)
        results.add(base+base+"123")

        # عربي انجليزي
        for ar in arabic:
            results.add(base+ar)

        # شائع
        results.add(base+"@123")
        results.add(base+"123!")
        results.add(base+"_123")

    return list(results)

# =========================
# Generate Passwords
# =========================
def generate_passwords(data,file_path):

    fields=[v.lower() for v in data.values() if v.strip()]
    var_lists=[variants(f) for f in fields]

    count=0

    with open(file_path,"w",encoding="utf-8") as f:

        # كلمات منفردة
        for v in var_lists:
            for pwd in v:
                f.write(pwd+"\n")
                count+=1

        # دمج كلمتين
        for i in range(len(var_lists)):
            for j in range(len(var_lists)):
                if i!=j:
                    for a in var_lists[i]:
                        for b in var_lists[j]:
                            f.write(a+b+"\n")
                            count+=1

        # انماط جاهزة
        COMMON=[
        "123456","12345678","123123","123qwe",
        "qwerty","qwerty123","1q2w3e4r",
        "zaq12wsx","asdf123","000000","111111"
        ]

        for c in COMMON:
            f.write(c+"\n")
            count+=1

        # الكود القديم
        for field in fields:
            f.write(field+"123\n")
            f.write(field+"1234\n")
            f.write(field+"2024\n")
            f.write(field+"2025\n")
            count+=4

    return count

# =========================
# Main
# =========================
def main():

    banner()

    keys=[
    "First Name","Last Name","Nickname","Known As","Old Username",
    "Mother Name","Father Name","Brother Name","Sister Name",
    "Person You Love","Best Friend","Pet Name",
    "Age","Birth Day","Birth Month","Birth Year","Graduation Year","Important Date",
    "City","District","School","University","Workplace",
    "Favorite Club","Favorite Player","Favorite Singer","Favorite Movie","Favorite Series","Favorite Game",
    "Lucky Number","Favorite Number","Phone Last 4 Digits","Street Number","Apartment Number",
    "Instagram Username","Facebook Username","Email Username"
    ]

    print("\nFill info (press Enter to skip)\n")

    data={}
    for k in keys:
        val=input(f"{k}: ").strip()
        if val:
            data[k]=val

    # تواريخ مركبة
    if "Birth Day" in data and "Birth Month" in data:
        data["Birth_DDMM"]=data["Birth Day"]+data["Birth Month"]

    if "Birth Year" in data:
        data["Birth_YY"]=data["Birth Year"][2:]

    # كلمات مخصصة
    print("\nAdd your own words (Enter empty to finish)")
    i=0
    while True:
        w=input("Add word: ").strip()
        if w=="":
            break
        data[f"Custom_{i}"]=w
        i+=1

    path=input("\nEnter save folder path: ").strip()
    os.makedirs(path,exist_ok=True)

    file_path=os.path.join(path,"MH_PASSWORDS.txt")

    count=generate_passwords(data,file_path)

    print("\nDone!")
    print("Generated:",count,"passwords")
    print("Saved to:",file_path)

if __name__=="__main__":
    main()
