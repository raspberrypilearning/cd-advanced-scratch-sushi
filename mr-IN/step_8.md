## लेवल 2

या चरणात, आपण खेळात एक नवीन लेव्हल जोडत आहात ज्यावर फक्त एक बटण दाबून खेळाडू पोचू शकेल. नंतर, आपल्या कोड मध्ये बदल करू शकता जेणेकरून त्यांना तेथे पोचण्यासाठी विशिष्ट संख्येची गुण किंवा काहीतरी दुसरे आवश्यक आहे.

### पुढील लेव्हल वर जाणे

\--- task \---

प्रथम, एक तर लायब्ररीतून एक स्प्राइट जोडून किंवा आपले लेव्हलचे रेखांकन करून बटण म्हणून नवीन sprite तयार करा. मी दोन्ही पैकी थोडे केले आणि यासह आलो:

![लेव्हल स्विच करण्यासाठी button sprite](images/levelButton.png)

\--- /task \---

\--- task \---

आता या बटणाचा कोड हुशार आहे: ते असे डिझाइन केले गेले आहे की प्रत्येक वेळी आपण त्यावर क्लिक केल्यावर कितीही लेव्हल असले तरीही ते आपल्याला पुढच्या लेव्हलवर घेऊन जाईल.

ही स्क्रिप्ट आपल्या ** Button** स्प्राइट मध्ये जोडा. असे करतांना आपल्याला काही व्हेरीएबल्स तयार करण्याची आवश्यकता असेल.

```blocks3
+    when green flag clicked
+    set [max-level v] to [2]
+    set [min-level v] to [1]
+    set [current-level v] to [1]
```

```blocks3
+    when this sprite clicked
+    change [current-level v] by (1)
+    if <(current-level) > (max-level ::variables)> then
        set [current-level v] to (min-level ::variables)
    end
+    broadcast [collectable-cleanup v]
+    broadcast (join [level-](current-level))
```

\--- /task \---

आपण तयार केलेल्या व्हेरीएबल्सचा प्रोग्राम कसा वापर करेल हे आपण पाहू शकता?

+ `max-level`{:class="block3variables"} सर्वात उंच्च लेव्हल संचयित करते
+ `min-level`{:class="block3variables"} सर्वात खालच्या लेव्हलला संचयित करते
+ `current-level`{:class="block3variables"} खेळाडू सध्या असलेल्या लेव्हल ला संचयित करते

हे सर्व प्रोग्रामर \(तुम्ही!\) द्वारे सेट करणे आवश्यक आहे, म्हणून जर आपण एखादे तृतीय लेव्हल जोडले तर `max-level`{:class="block3variables"} चे मूल्य बदलायला विसरु नका! `min-level`{:class="block3variables"} नक्कीच कधीही बदलण्याची आवश्यकता नाही.

प्रसारण (ब्रॉडकास्ट) चा वापर इतर स्प्राइट्सना कोणता लेव्हल दर्शवायचा हे दर्शविण्या साठी आणि नवीन लेव्हल सुरू झाल्यावर कलेक्टेबल्स काढून टाकण्या साठी होतो.

### स्प्राइट्सला प्रतिक्रिया द्यायला लावा

#### **Collectable** स्प्राइट

आता आपल्याला इतर स्प्राइट्सला या प्रसारणाला प्रतिसाद द्यायला लावायचे आहे! सर्वात सोपे सह प्रारंभ करा: सर्व कलेक्टेबल्स साफ करणे.

\--- task \---

क्लीनअप ब्रॉडकास्ट प्राप्त झाल्यावर त्यांचे सर्व प्रत्यांना `hide`{:class="block3vlooks"} व्हायला सांगण्यासाठी **Collectable** स्प्राइट स्क्रिप्ट मध्ये खालील कोड जोडा:

```blocks3
+    when I receive [collectable-cleanup v]
+    hide
```

\--- /task \---

कोणताही नवीन प्रत प्रथम गोष्टीं पैकी एक म्हणजे तो स्वत: ला दर्शवितो, आपल्याला कलेक्टेबल दर्शविण्याची चिंता करण्याची गरज नाही!

#### **Platforms** स्प्राइट

आता **Platforms** स्प्राइट बदलायचे आहे. आपण इच्छित असल्यास आपण आपल्या स्वत: च्या नवीन स्तराची रचना नंतर करू शकता, परंतु आत्तासाठी मी आधीपासून समाविष्ट केलेला वापर करू - आपण पुढील स्टेप मध्ये का ते पहाल!

\--- task \---

हा कोड **Platforms** स्प्राइट मध्ये जोडा:

```blocks3
+    when I receive [level-1 v]
+    switch costume to [Level 1 v]
+    show
```

```blocks3
+    when I receive [level-2 v]
+    switch costume to [Level 2 v]
+    show
```

\--- /task \---

हे `level-`{:class="block3variables"} आणि `current-level`{:class="block3variables"} चे `joined`{:class="block3operators"} संदेश प्राप्त करते जे **Button** स्प्राइट्सनी पाठवले असते आणि ** Platforms** चे कोस्ट्यूम्स बदलून प्रतिसाद देते.

#### **Enemy** स्प्राइट

\--- task \---

**Enemy** स्प्राइट स्क्रिप्टमध्ये, जेव्हा खेळाडू लेव्हल 2 मध्ये प्रवेश करतो तेव्हा स्प्राइट अदृश्य होईल याची खात्री करा:

```blocks3
+    when I receive [level-1 v]
+    show
```

```blocks3
+    when I receive [level-2 v]
+    hide
```

\--- /task \---

आपण प्राधान्य दिल्यास, त्याऐवजी आपण शत्रूला दुसर्‍या प्लॅटफॉर्मवर हलवू शकता. त्या परिस्थितीत, आपण `show`{:class="block3looks"} आणी `hide`{:class="block3looks"} ब्लॉक्सच्या ऐवजी `go to`{:class="block3motion"} ब्लॉकचा वापर कराल.

### **Player Character** योग्य ठिकाणी दिसेल तसे करा

जेव्हा जेव्हा एखादी नवीन लेव्हल सुरू होते, तेव्हा त्या लेव्हलसाठी **Player Character** स्प्राइट ला योग्य ठिकाणी जाणे आवश्यक असते. हे घडवून आणण्यासाठी, जेव्हा स्प्राइट स्टेजवर प्रथम येईल तेव्हा त्याला त्याचे निर्देशांक कुठून मिळतील हे बदलणे आवश्यक आहे. याक्षणी, त्यामधील कोडमध्ये `x` and `y` मूल्ये निश्चित आहेत.

\--- task \---

प्रारंभिक निर्देशांकांसाठी व्हेरिएबल्स तयार करुन प्रारंभ करा: `start-x`{:class="block3variables"} आणी `start-y`{:class="block3variables"}. नंतर `x` आणी `y` असे निश्चित मूल्यांच्या ऐवजी त्यांना `reset-character`{:class="block3myblocks"} **My blocks** ब्लॉक मधील `go to`{:class="block3motion"} ब्लॉक मध्ये प्लग करा:

```blocks3
    define reset-character
    set [can-jump v] to [true]
    set [x-velocity v] to [0]
    set [y-velocity v] to [-0]
+    go to x: (start-x) y: (start-y)
```

\--- /task \---

\--- task \---

नंतर प्रत्येक लेव्हल सुरू होण्याची घोषणा करणाऱ्या ब्रॉडकास्ट साठी, योग्य `start-x`{:class="block3variables"} आणी `start-y`{:class="block3variables"} निर्देशांक सेट करा आणि `reset-character`{:class="block3myblocks"} साठी एक **कॉल** जोडा:

```blocks3
+    when I receive [level-1 v]
+    set [start-x v] to [-183]
+    set [start-y v] to [42]
+    reset-character :: custom
```

```blocks3
+    when I receive [level-2 v]
+    set [start-x v] to [-218]
+    set [start-y v] to [-143]
+    reset-character :: custom
```

\--- /task \---

### लेव्हल 1 पासून सुरुआत

आपल्याला हे देखील सुनिश्चित करण्याची आवश्यकता आहे की प्रत्येक वेळी कोणी ही गेम सुरू करेल, तेव्हा ते खेळत असलेले प्रथम लेव्हल, लेव्हल 1 आहे.

\--- task \---

`reset-game`{:class="block3myblocks"} स्क्रिप्टवर जा आणि त्यामधून `reset-character`{:class="block3myblocks"} वरचा कॉल काढा. त्याच्या जागी `min-level`{:class="block3variables"} चं प्रसारण करा. या कार्डासह आपण जो कोड जोडला आहे ते**Player Character** स्प्राइट साठी योग्य प्रारंभिक समन्वय स्थापित करेल आणि`reset-character`{:class="block3myblocks"} देखील कॉल करेल.

```blocks3
    define reset-game
    set rotation style [left-right v]
    set [jump-height v] to [15]
    set [gravity v] to [2]
    set [x-speed v] to [1]
    set [y-speed v] to [1]
    set [lives v] to [3]
    set [points v] to [0]
+    broadcast (join [level-](min-level ::variables))
```

\--- /task \---

## \--- collapse \---

## title: प्लेअर कॅरेक्टर रीसेट करणे विरुद्ध गेम रीसेट करणे

लक्षात घ्या की **Player Character** स्प्राइट च्या मुख्य हिरव्या ध्वजांकित स्क्रिप्ट मधील पहिला ब्लॉक म्हणजे `reset-game`{:class="block3myblocks"} **My blocks** ब्लॉक ला कॉल आहे.

हे ब्लॉक नवीन गेमसाठी सर्व व्हेरिएबल्स सेट अप करते आणि नंतर `reset-character`{:class="block3myblocks"} **My blocks** ब्लॉकला कॉल करते, जे केरेक्टर ला परत त्याच्या योग्य सुरूवातीच्या जागी ठेवते.

`reset-character`{:class="block3myblocks"} कोडला स्वतःच्या ब्लॉक मध्ये, `reset-game`{:class="block3myblocks"} पासून वेगळे, ठेवणे आपल्याला पूर्ण गेम रीसेट **न** करता भिन्न स्थितीत केरेक्टर रीसेट करण्यास अनुमती देते.

\--- /collapse \---