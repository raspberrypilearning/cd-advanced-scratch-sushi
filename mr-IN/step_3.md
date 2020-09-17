## खेळ हरणे

प्रथम गोष्टी प्रथम! जेव्हा खेळाडूचे जीवने संपतील तेव्हा आपल्याला गेम समाप्त करण्याचा मार्ग शोधून काढायचा आहे. या क्षणी तसं होणार नाही.

आपणास हे लक्षात आले असेल की **Player Character** स्प्राइट च्या स्क्रीप मध्ये `lose`{:class="block3myblocks"} **My blocks** ब्लॉक रिक्त आहे. आपण हे मध्ये भरणार आहात आणि छान 'गेम ओव्हर' स्क्रीनसाठी आवश्यक असलेले सर्व तुकडे सेट-अप कराल.

--- task ---

प्रथम, `lose`{:class="block3myblocks"} ब्लॉक शोधा आणि खालील कोडसह ते पूर्ण करा:

```blocks3
    define lose
+    stop [other scripts in sprite v] :: control stack
+    broadcast [game over v]
+    go to x:(0) y:(0)
+    say [Game over!] for (2) secs
+    stop [all v]
```

--- /task ---

--- collapse ---
---
title: हा कोड काय करतो?
---

जेव्हा `lose`{:class="block3myblocks"} ब्लॉक चालते, तेव्हा ते हे करते:

1. **Player Character**वर कार्य करणारी फिज़िक्स आणि अन्य गेम स्क्रिप्ट थांबवते
2. एक `game over`{:class="block3events"} संदेश **broadcasting** करून इतर सर्व स्प्राइट्सला खेळ संपल्याचे सांगते, ज्याला ते प्रतिसाद देऊ शकतात आणि ते काय करत आहेत ते बदलू शकतात
3. **Player Character**स्टेजच्या मध्यभागी हलवते आणि खेळ संपला आहे असे खेळाडूला सांगते
4. गेम मधील सर्व स्क्रीप्ट थांबवते

--- /collapse ---

आता आपल्याला हे सुनिश्चित करण्याची आवश्यकता आहे की सर्व स्प्राइट्सना हा गेम संपल्यावर काय करावे आणि खेळाडू नवीन गेम सुरू करतात तेव्हा स्वतःला कसे रीसेट करावे हे माहित आहे. ** हे विसरू नका की आपण जोडलेल्या कोणत्याही नवीन स्प्राइट्सना देखील यासाठी कोड आवश्यक असू शकेल!**

### प्लॅटफॉर्म आणि काठ लपविणे

--- task ---

सर्वात सोप असलेल्या स्प्राइट्स पासून शुरुआत करा. गेम सुरू होताना दिसण्यासाठी आणि `game over`{:class="block3events"} प्रसारण प्राप्त झाल्यावर अदृश्य होण्यासाठी **Platforms**आणि **Edges** दोघांनाही कोडची आवश्यकता आहे. म्हणून त्या प्रत्येकात हे ब्लॉक्स जोडा:

```blocks3
+    when I receive [game over  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

--- /task ---

### ता-यांना थांबवणे

आता, आपण **Collectable** स्प्राइट साठीचे कोड पाहिल्यास, ते स्वतः चे **प्रत** बनवून कार्य करत असल्याचे आपल्यास आढळेल. म्हणजेच, त्या स्वत: च्या प्रती बनवितात ज्या विशेष `when I start as a clone`{:class="block3events"} सूचनांचे अनुसरण करतात.

जेव्हा आपण नवीन आणि भिन्न संग्रहणीय बनवण्याच्या चरणात पोहोचु तेव्हा प्रत्यांचे काय वैशिष्ठ्य आहे याबद्दल अधिक बोलू. आत्तासाठी, आपल्याला हे माहित असणे आवश्यक आहे की प्रत्या, `broadcast`{:class="block3events"} संदेश प्राप्त करण्यासह सामान्य स्प्राईट **जवळ-जवळ** सर्व काही करु शकतात.

**Collectable** स्प्राइट कसे कार्य करते ते पहा. आपण त्यातील काही कोड समजू शकता की नाही ते पहा:

```blocks3
    when green flag clicked
    hide
    set [collectable-value v] to [1]
    set [collectable-speed v] to [1]
    set [collectable-frequency v] to [1]
    set [create-collectables v] to [true]
    set [collectable-type v] to [1]
    repeat until <not <(create-collectables) = [true]>>
        wait (collectable-frequency) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [myself v]
    end
```

1. प्रथम ते मूळ **Collectable** स्प्राइट लपवून अदृश्य करतं
2. नंतर ते नियंत्रण व्हेरिएबल्सची स्थापना करते - आपण यावर नंतर परत येऊ
3. `create-collectables`{:class="block3variables"} क्लोनिंग चालू/बंद करण्याची स्विच आहे: `create-collectables`{:class="block3variables"} `true` असल्यास लूप क्लोन तयार करते, आणि तसे नसल्यास काही करत नाही

--- task ---

आता **Collectable** स्प्राइट साठी एक ब्लॉक सेट-अप करा जेणेकरून ते `game over` प्रसारण वर प्रतिक्रिया देईल:

```blocks3
+    when I receive [game over v]
+    hide
+    set [create-collectables v] to [false]
```

--- /task ---

हा कोड **Platforms** आणि **Edges** sprites नियंत्रित करणार्‍या कोड सारखेच आहे. फरक एवढाच आहे की आपण `create-collectables`{:class="block3variables"} व्हेरिएबल `false` असे देखील सेट करत आहात जेणेकरून जेव्हा गेम संपते तेव्हा कोणते ही नवीन क्लोन तयार होणार नाहीत.

लक्षात घ्या की आपण `create-collectables`{:class="block3variables"} व्हॅरिएबल चा वापर करून कोड च्या एका भागामधून दुसर्‍या भागात संदेश पाठवू शकता!