# 📅 Week 2

This is Week 2 of my rising senior year. I started learning the C programming language last week and am getting closer to buying my first Arduino kit. I'm beginning to feel more confident in my coding journey and staying deeply focused on my future goals.

My school is organizing a summer internship opportunity for students like me to help build confidence and encourage collaboration. I believe this summer is going to be different — I can already feel it.

For this week, my goals are:
- Complete learning the basics of C
- Purchase the Arduino kit
- Join a volunteering community
- Pinpoint my dream universities

---

# 🗓️ Week 3–8 Update

Although I didn’t document my progress weekly, I’ve been active behind the scenes! Over the past few weeks, I’ve focused on strengthening my programming skills through consistent practice and small experiments — especially with JavaScript, Arduino, and web development tools.

I am also participating in the **Zemenay Tech Solutions Hackathon**, where I work on building a modular blog system. The goal is to create a blog solution that integrates easily with any Next.js frontend, using Supabase and PostgreSQL on the backend. It is a great chance to apply my learning and collaborate on real-world code.

In Week 8, I also started recording devlog-style videos to reflect on my progress and stay accountable — a small step toward better documentation and sharing.

📽️ **Devlog Video:** [Watch Week 8 Devlog](https://drive.google.com/file/d/1Pz-MRVNDm3wAU08N0yfDR6WZwy9m_703/view?usp=drivesdk)

# 5161AS 7-Segment Display Counter Project(Week 9-14)

## Project Context

This project was originally planned as part of the **Zemenay Tech Solutions Hackathon**.  
However, I was unable to fully work on it during the hackathon because I traveled to the United States and school commitments over the past few weeks kept me busy. Despite these challenges, I continued experimenting independently, which led to this 7-segment display project.

---

## Project Overview

A **0–9 counter** using a **5161AS common cathode 7-segment display** with an **Arduino Uno**.

**Features:**
- Counts **0–9 sequentially**.
- **0** stays longer on display with the **decimal point** illuminated.
- Each segment protected with a **series resistor**.
- Clear **pin-to-segment mapping** for easy wiring.

---

## Hardware Setup

| Segment | Arduino Pin |
|---------|------------|
| a       | 7          |
| b       | 6          |
| c       | 4          |
| d       | 3          |
| e       | 2          |
| f       | 8          |
| g       | 9          |
| DP      | 5          |

> Commons → **GND**  
> Use **330 Ω resistors** for each segment and DP.

---

## Arduino Code

```cpp
// Pins for segments a–g
const int segmentPins[7] = {7,6,4,3,2,8,9}; // a,b,c,d,e,f,g
const int dpPin = 5; // Decimal Point

// Digits 0–9 mapping (a,b,c,d,e,f,g)
const int digits[10][7] = {
  {1,1,1,1,1,1,0}, // 0
  {0,1,1,0,0,0,0}, // 1
  {1,1,0,1,1,0,1}, // 2
  {1,1,1,1,0,0,1}, // 3
  {0,1,1,0,0,1,1}, // 4
  {1,0,1,1,0,1,1}, // 5
  {1,0,1,1,1,1,1}, // 6
  {1,1,1,0,0,0,0}, // 7
  {1,1,1,1,1,1,1}, // 8
  {1,1,1,1,0,1,1}  // 9
};

void setup() {
  for(int i=0; i<7; i++) pinMode(segmentPins[i], OUTPUT);
  pinMode(dpPin, OUTPUT);
}

void loop() {
  for(int num=0; num<10; num++){
    displayNumber(num);

    // Light DP only for 0
    if(num == 0){
      digitalWrite(dpPin, HIGH);   // DP ON
      delay(3000);                 // 0 stays 3 seconds
      digitalWrite(dpPin, LOW);    // DP OFF
    } else {
      digitalWrite(dpPin, LOW);    // DP OFF
      delay(1000);                 // Other numbers 1s
    }
  }
}

void displayNumber(int num){
  for(int i=0; i<7; i++){
    digitalWrite(segmentPins[i], digits[num][i]);
  }
}


