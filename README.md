# jackofheist
first collaborated project
with
ghoshrudramadhab-debug
JACK-OF-HEIST


ALL REQUIRED LIBRARIES
import os<br> import time<br> import random from twilio.rest<br> import Client import cv2 from PIL<br> import Image<br> import numpy as np<br>

INITIALIZE TOTAL CREDIT TRACKERS
listforplayer11 = 0 listforplayer22 = 0 listforplayer33 = 0 listforplayer44 = 0

GAME INTRODUCTION
print("JACK OF HEIST X_X௹ by SANGRAM PANIGRAHI & RUDRA MADHAB GHOSH") print() time.sleep(2) print("WeLCoMe! TO THE WORLD OF HeIsT👹") time.sleep(2) print() print("Press 69 to start..", end=" ") r = int(input()) if r == 69: print() print("Lets get started!") print() time.sleep(2) print("Loading...") time.sleep(3) print() print("It's rules time!") print()

print("1. ONLY FOUR PLAYERS ARE ALLOWED TO PLAY THIS GAME AT A SINGLE TIME")
time.sleep(1)
print("2. EACH PLAYER HAS TO ENTER HIS/HER NAME AND WHATSAPP NUMBER BEFORE STARTING TO PLAY")
time.sleep(1)
print("3. EACH PLAYER WILL BE ASSIGNED SOME CRADITS AND A COLOR CARD TO START WITH")
time.sleep(1)
print("4. EACH PLAYER WILL BE ASSIGNED A CHARACTER {i.e KING, QUEEN, KNIGHT OR JACK} SECRETLY AND WONT BE REVEALED TO PLAYERS")
time.sleep(1)
print("5. THE WEBCAM OF THE DEVICE WILL START AND RECOGNISE THE COLOR OF THE PLAYER'S CARD")
time.sleep(1)
print("6. EACH PLAYER WULL BE SENT A WHATSAPP MESSAGE REVEALING HIS/HER CHARACTER BASED ON THE COLOR OF THE CARD HE/SHE HOLDS INFRONT OF THE WEBCAM")
time.sleep(1)
print("7. ONLY THE KNIGHT'S NAME WILL BE DISPLAYED ON THE SCREEN")
time.sleep(1)
print("8. THE KNIGHT HAS TO GUESS THE JACK AMONGST THE PLAYERS")
time.sleep(1)
print("9. IF THE KNIGHT GUESSES IT RIGHT, HIS CREDITS WILL BE RESERVED ")
time.sleep(1)
print("10. IF THE KNIGHT GUESSES IT WRONG, THE JACK WILL STEAL WHOLE CREDITS FROM THE KNIGHT")
time.sleep(1)
print("11. AFTER WHATEVER ROUNG YOU WISH TO PLAY, THE GAME WILL TERMINATE & THE PLAYER WITH HIGHEST CREDITS WILL BE DECLARED AS THE WINNER")
time.sleep(1)
print()
print("PRESS 1 TO CONTINUE...", end=" ")
print()
r2 = int(input())
if r2 == 1:
    print("LOADING...")
    time.sleep(2)
print("ENJOY THE GAME!🤩") time.sleep(1) print()

PLAYER DETAILS INPUT
print("PLEASE ENTER THE NAME OF PLAYER 1:", end=" ") p1 = input() P1_NUMBER= "whatsapp:"+ input("PLEASE ENTER YOUR WHATSAPP NUMBER WITH COUNTRY CODE: ") print()

print("PLEASE ENTER THE NAME OF PLAYER 2:", end=" ") p2 = input() P2_NUMBER= "whatsapp:"+ input("PLEASE ENTER YOUR WHATSAPP NUMBER WITH COUNTRY CODE: ") print()

print("PLEASE ENTER THE NAME OF PLAYER 3:", end=" ") p3 = input() P3_NUMBER= "whatsapp:"+ input("PLEASE ENTER YOUR WHATSAPP NUMBER WITH COUNTRY CODE: ") print()

print("PLEASE ENTER THE NAME OF PLAYER 4:", end=" ") p4 = input() P4_NUMBER= "whatsapp:"+ input("PLEASE ENTER YOUR WHATSAPP NUMBER WITH COUNTRY CODE: ") print()

MAIN GAME LOOP FOR MULTIPLE ROUNDS
while True: generalvalues = [400, 600, 700, 900] generalcolors = ["RED", "GREEN", "YELLOW", "MAGENTA"] random.shuffle(generalcolors) color1 = generalcolors[0] color2 = generalcolors[1] color3 = generalcolors[2] color4 = generalcolors[3]

valueforking = 1000
valueforjack = 0

roles = ["KING", "QUEEN", "KNIGHT", "JACK"]
random.shuffle(roles)

listforplayer1 = []
listforplayer1.append(p1)
listforplayer1.append(roles[0])
listforplayer1.append(color1)
listforplayer1.append(color1)
listforplayer1.append(valueforking if roles[0] == "KING" else valueforjack if roles[0] == "JACK" else random.choice(generalvalues))

listforplayer2 = []
listforplayer2.append(p2)
listforplayer2.append(roles[1])
listforplayer2.append(color2)
listforplayer2.append(color2)
listforplayer2.append(valueforking if roles[1] == "KING" else valueforjack if roles[1] == "JACK" else random.choice(generalvalues))

listforplayer3 = []
listforplayer3.append(p3)
listforplayer3.append(roles[2])
listforplayer3.append(color3)
listforplayer3.append(color3)
listforplayer3.append(valueforking if roles[2] == "KING" else valueforjack if roles[2] == "JACK" else random.choice(generalvalues))

listforplayer4 = []
listforplayer4.append(p4)
listforplayer4.append(roles[3])
listforplayer4.append(color4)
listforplayer4.append(color4)
listforplayer4.append(valueforking if roles[3] == "KING" else valueforjack if roles[3] == "JACK" else random.choice(generalvalues))

ACCOUNT_SID = " "
AUTH_TOKEN  = " "
TWILIO_WHATSAPP_NUMBER = "whatsapp:+14155238886" 

client = Client(ACCOUNT_SID, AUTH_TOKEN)

print()
print("WEBCAM SCANNING WILL START NOW...")
print()
print("TAKE A WHITE BACKGROUNG FOR BETTER DETECTION")
time.sleep(2)

players = [p1, p2, p3, p4]
colors = [color1, color2, color3, color4]
PLAYERS_NUMBER= [P1_NUMBER, P2_NUMBER, P3_NUMBER, P4_NUMBER]

color_ranges = {
    "RED":     ((0, 120, 70), (10, 255, 255)),
    "GREEN":   ((35, 80, 80), (85, 255, 255)),
    "YELLOW":  ((20, 100, 100), (35, 255, 255)),
    "MAGENTA": ((140, 80, 80), (170, 255, 255))
}

x, y, w, h = 100, 150, 200, 200

for i in range(4):
    print(f"{players[i]}, show your {colors[i]} card")
    cap = cv2.VideoCapture(0)
    lower, upper = color_ranges[colors[i]]

    while True:
        ret, frame = cap.read()
        if not ret:
            break
        hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
        mask = cv2.inRange(hsv, np.array(lower), np.array(upper))
        roi_mask = mask[y:y+h, x:x+w]

        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
        cv2.putText(frame, f"{players[i]}: Show {colors[i]} card", (30, 40), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (255, 255, 255), 1)

        if cv2.countNonZero(roi_mask) > 200:
            message= f"""
            🎴 JACK OF HEIST 🎴

            Name: {players[i]}
            Role: {roles[i]}
            Credits: {listforplayer1[4] if players[i]==p1 else listforplayer2[4] if players[i]==p2 else listforplayer3[4] if players[i]==p3 else listforplayer4[4]}
            Color Card: {colors[i]}

            ⚠️ Do NOT share this with other players!
            """
            client.messages.create(body=message, from_="whatsapp:+14155238886", to= PLAYERS_NUMBER[i])
            
            cv2.putText(frame, "COLOR DETECTED & MESSAGE SENT", (50, 90), cv2.FONT_HERSHEY_SIMPLEX, 1, (0, 255, 0), 3)
            cv2.imshow("Color Scan", frame)
            cv2.waitKey(1000)
            break

        cv2.imshow("Color Scan", frame)
        cv2.waitKey(50)   

    cap.release()
    cv2.destroyAllWindows()

print("✅ ALL PLAYERS VERIFIED SUCESSFULLY! PLEASE CHECK YOUR WHATSAPP FOR YOUR ROLES & CREDITS DETAILS.")
print("AND!! THE KNIGHT IS....")
time.sleep(5)
if listforplayer1[1] == "KNIGHT":
    print(f"{p1} is the KNIGHT")
elif listforplayer2[1] == "KNIGHT":
    print(f"{p2} is the KNIGHT")
elif listforplayer3[1] == "KNIGHT":
    print(f"{p3} is the KNIGHT")
elif listforplayer4[1] == "KNIGHT":
    print(f"{p4} is the KNIGHT")

newlis1=listforplayer1.copy()
newlis2=listforplayer2.copy()
newlis3=listforplayer3.copy()
newlis4=listforplayer4.copy()

time.sleep(2)
if(listforplayer1[1]=="KNIGHT"):
    print()
    print()
    time.sleep(2)
    a=input(f"{p1} PLEASE GUESS THE NAME OF THE PLAYER WHOME U THINK MIGHT BT THE JACK: ")
    if(listforplayer2[1]=="JACK" and a==listforplayer2[0]):
        print()
        print(f"Wooho!!! 🙌 {p1} WON!! , {listforplayer2[0]} IS INDEED THE JACK!!! 👹")
    elif(listforplayer3[1]=="JACK" and a==listforplayer3[0]):
        print()
        print(f"Wooho!!! 🙌 {p1} WON!! , {listforplayer3[0]} IS INDEED THE JACK!!! 👹")
    elif(listforplayer4[1]=="JACK" and a==listforplayer4[0]):
        print()
        print(f"Wooho!!!{p1} WON!! , {listforplayer4[0]} IS INDEED THE JACK!!! 👹")
    else:
        print()
        print("Uhh,ohh!" ,p1, " UUUU....LOST!! 👦,BETTER LUCKNEXT TIME!")
        time.sleep(3)
        print()        
        print()
        print("YOU KNOW! WHY I AM CALLED JACK👹....BECAUSE I STEAL....YOUR CREDITS ARE GONEEE!!👹💰")
        listforplayer1[4] = 0
        if(listforplayer2[1]=="JACK"):
            listforplayer2[4] = listforplayer2[4] + newlis1[4]
        elif(listforplayer3[1]=="JACK"):
            listforplayer3[4] = listforplayer3[4] + newlis1[4]
        elif(listforplayer4[1]=="JACK"):
            listforplayer4[4] = listforplayer4[4] + newlis1[4]

elif(listforplayer2[1]=="KNIGHT"):
    print()
    print()
    time.sleep(2)
    b=input(f"{p2} PLEASE GUESS THE NAME OF THE PLAYER WHOME U THINK MIGHT BE THE JACK: ")
    if(listforplayer1[1]=="JACK" and b==listforplayer1[0]):
        print()
        print(f"Wooho!!!{p2} WON!! 🙌 , {listforplayer1[0]} IS INDEED THE JACK 👹")
    elif(listforplayer3[1]=="JACK" and b==listforplayer3[0]):
        print()
        print(f"Wooho!!!{p2} WON!! 🙌, {listforplayer3[0]} IS INDEED THE JACK 👹")
    elif(listforplayer4[1]=="JACK" and b==listforplayer4[0]):
        print()
        print(f"Wooho!!!{p2} WON!! 🙌,{listforplayer4[0]} IS INDEED THE JACK 👹")
    else:
        print()
        print("Uhh,ohh!",p2,"UUUU....LOST!! 👦,BETTER LUCK NEXT TIME!")
        time.sleep(3)
        print()
        print("YOU KNOW! WHY I AM CALLED JACK👹....BECAUSE I STEAL....YOUR CREDITS ARE GONEEE!!👹💰")
        listforplayer2[4] = 0
        if(listforplayer1[1]=="JACK"):
            listforplayer1[4] = listforplayer1[4] + newlis2[4]
        elif(listforplayer3[1]=="JACK"):
            listforplayer3[4] = listforplayer3[4] + newlis2[4]
        elif(listforplayer4[1]=="JACK"):
            listforplayer4[4] = listforplayer4[4] + newlis2[4]

elif(listforplayer3[1]=="KNIGHT"):
    print()
    print()
    time.sleep(2)
    c=input(f"{p3} PLEASE GUESS THE NAME OF THE PLAYER WHOME U THINK MIGHT BE THE JACK: ")
    if(listforplayer2[1]=="JACK" and c==listforplayer2[0]):
        print()
        print(f"Wooho!!!  🙌 {p3} WON!! ,{listforplayer2[0]} IS INDEED THE JACK👹")
    elif(listforplayer1[1]=="JACK" and c==listforplayer1[0]):
        print()
        print(f"Wooho!!! 🙌 {p3} WON!! ,{listforplayer1[0]} IS INDEED THE JACK👹")
    elif(listforplayer4[1]=="JACK" and c==listforplayer4[0]):
        print()
        print(f"Wooho!!! 🙌 {p3} WON!! ,{listforplayer4[0]} IS INDEED THE JACK👹")
    else:
        print()
        print("Uhh,ohh!",p3,"UUUU....LOST!! 👦,BETTER LUCK NEXT TIME!")
        time.sleep(3)
        print()
        print()
        print("You know! Why I am called Jack👹....because I steal....your credits are goneee!!👹💰")
        listforplayer3[4] = 0
        if(listforplayer2[1]=="JACK"):
            listforplayer2[4] = listforplayer2[4] + newlis3[4]
        elif(listforplayer1[1]=="JACK"):
            listforplayer1[4] = listforplayer1[4] + newlis3[4]
        elif(listforplayer4[1]=="JACK"):
            listforplayer4[4] = listforplayer4[4] + newlis3[4]

elif(listforplayer4[1]=="KNIGHT"):
    print()
    print(f"{p4}, YOU GOTTA CHOOSE THE JACK👹")
    print()
    time.sleep(2)
    d=input(f"{p4} PLEASE GUESS THE NAME OF THE PLAYER WHOME U THINK MIGHT BE THE JACK👹: ")
    if(listforplayer2[1]=="JACK" and d==listforplayer2[0]):
        print()
        print(f"Wooho!!! 🙌 {p4} WON!, {listforplayer2[0]} IS THE JACK, ACTUALLY")
    elif(listforplayer3[1]=="JACK" and d==listforplayer3[0]):
        print()
        print(f"Wooho!!! 🙌 {p4} WON!,{listforplayer3[0]} IS THE JACK, ACTUALLY")
    elif(listforplayer1[1]=="JACK" and d==listforplayer1[0]):
        print()
        print(f"Wooho!!! 🙌 {p4} WON!, {listforplayer1[0]} IS THE JACK, ACTUALLY")
    else:
        print()
        print("Uhh,ohh!" ,p4, "UUU....LOST 🤦‍♂️, BETTER LUCK NEXT TIME😔")
        print()
        print("YOU KNOW! WHY I AM CALLED JACK👹....BECAUSE I STEAL....YOUR CREDITS ARE GONEEE!!👹💰")
        listforplayer4[4] = 0
        if(listforplayer2[1]=="JACK"):
            listforplayer2[4] = listforplayer2[4] + newlis4[4]
        elif(listforplayer1[1]=="JACK"):
            listforplayer1[4] = listforplayer1[4] + newlis4[4]
        elif(listforplayer3[1]=="JACK"):
            listforplayer3[4] = listforplayer3[4] + newlis4[4]

# UPDATE GRAND TOTALS
listforplayer11 += listforplayer1[4]
listforplayer22 += listforplayer2[4]
listforplayer33 += listforplayer3[4]
listforplayer44 += listforplayer4[4]

print("IF YOU WISH TO PLAY ANOTHER ROUND, PRESS 69 ELSE PRESS 0 TO TERMINATE THE GAME: ", end=" ")
r3 = int(input())
if r3 == 69:
    print("LOADING NEXT ROUND...")
    time.sleep(5)
else:
    print("TERMINATING THE GAME...")
    time.sleep(3)
    print("AND THE WINNER IS....")
    time.sleep(2)
    if (listforplayer11 > listforplayer22) and (listforplayer11 > listforplayer33) and (listforplayer11 > listforplayer44):
        print(f"CONGRATS {p1} YOU ARE THE WINNER WITH {listforplayer11} CREDITS 🏆🎉")
    elif (listforplayer22 > listforplayer11) and (listforplayer22 > listforplayer33) and (listforplayer22 > listforplayer44):
        print(f"CONGRATS {p2} YOU ARE THE WINNER WITH {listforplayer22} CREDITS 🏆🎉")
    elif (listforplayer33 > listforplayer11) and (listforplayer33 > listforplayer22) and (listforplayer33 > listforplayer44):
        print(f"CONGRATS {p3} YOU ARE THE WINNER WITH {listforplayer33} CREDITS 🏆🎉")
    elif (listforplayer44 > listforplayer11) and (listforplayer44 > listforplayer22) and (listforplayer44 > listforplayer33):
        print(f"CONGRATS {p4} YOU ARE THE WINNER WITH {listforplayer44} CREDITS 🏆🎉")
    break
#About
#This is a real-time AI COMPUTER VISION enabled game, with a real-time WhatsApp integrity

