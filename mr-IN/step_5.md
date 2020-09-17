## सुपर पॉवर-अप!

आता आपल्याकडे नवीन पॉवर-अप कलेक्टेबल तयार झाले आहे, आता काहीतरी खरोखर छान करण्याची वेळ आली आहे: केवळ एक अतिरिक्त जीवन न देता काही सेकंदांसाठी पॉवर-अप चा 'वर्षाव' करू या.

या साठी आपण आणखी एक `broadcast`{:class="block3events"} संदेश वापरणार आहात.

\--- task \---

प्रथम, प्लेयर केरेक्टर `2` कलेक्टेबल ला स्पर्श करते तेव्हा संदेश प्रसारित करण्यासाठी `react-to-player`{:class="block3myblocks"} ब्लॉक बदला. संदेशास `collectable-rain` {:class="block3events"} असं नाव द्या.

```blocks3
    define react-to-player (type)
    if <(type ::variable) = [1]> then
        change [points v] by (collectable-value ::variables)
    end
    if <(type ::variable) = [2]> then
-        change [lives v] by [1]    
+        broadcast [collectable-rain v]
    end
```

\--- /task \---

आता आपणास **Collectable** स्प्राईट स्क्रिप्ट मध्ये कोडचा एक नवीन भाग तयार करणे आवश्यक आहे जे जेव्हा `collectable-rain`{:class="block3events"} संदेश प्रसारित होते तेव्हा सुरू होईल.

\--- task \---

`collectable-rain`{:class="block3events"} प्रसारणासाठी ऐकू येण्या करिता **Collectable** स्प्राईट साठी हा कोड जोडा.

```blocks3
+    when I receive [collectable-rain v]
+    set [collectable-frequency v] to [0.000001]
+    wait (1) secs
+    set [collectable-frequency v] to [1]
```

\--- /task \---

## \--- collapse \---

## title: नवीन कोड काय करते?

कोड चा हा भाग प्रसारण प्राप्त होण्याची प्रतीक्षा करतो आणि `collectable-frequency`{:class="block3variables"} व्हेरीएबल ला खूप लहान संख्येने सेट करून प्रतिसाद देतो, नंतर एक सेकंदाची वाट पहातो आणि नंतर बदललेला व्हेरीएबल परत `1` वर करतो.

`collectable-frequency`{:class="block3variables"} व्हेरिएबल कलेक्टेबलचा पाऊस कसा काय पाडतो हे शोधण्यासाठी आपण तो कसा वापरला जातोय हे पाहू.

मुख्य गेम लूपमध्ये **Collectable** स्प्राईटच्या प्रत बनविणार्‍या कोड चा भागाला `collectable-frequency`{:class="block3variables"} व्हेरिएबल द्वारे सांगितले जाते कि एक प्रत आणि दुसरी प्रत बनवण्यामध्ये किती वेळ थांबायचे आहे:

```blocks3
    repeat until <not <(create-collectables ::variables) = [true]>>
        if < [50] = (pick random (1) to (50))> then
            set [collectable-type v] to [2]
        else
            set [collectable-type v] to [1]
        end
        wait (collectable-frequency ::variables) secs
        go to x: (pick random (-240) to (240)) y:(179)
        create clone of [myself v]
    end
```

आपण पाहू शकता की `wait`{:class="block3control"} ब्लॉक <`collectable-frequency`{:class="block3variables"} द्वारे सेट केलेल्या लांबीसाठी कोड ला विराम देते.

`collectable-frequency`{:class="block3variables"} चे मूल्य जर `0.000001` असेल तर, `wait`{:class="block3control"} ब्लॉक केवळ सेकंदाच्या **दहा लाखव्या** भागासाठी विराम देतो, याचा अर्थ `repeat until`{:class="block3control"} लूप सामान्य पेक्षा जास्त वेळा चालेल. परिणामी, `collectable-frequency`{:class="block3variables"} परत `1` वर बदलल्या शिवाय कोड सामान्य पेक्षा **बरेच** अधिक पॉवर-अप तयार करेल.

आपण ह्या मधून उद्भवू शकणाऱ्या कोणत्याही समस्यांचा विचार करू शकता? तेव्हा बरेच पॉवर-अप्स असतील… आपण त्यांना पकडत राहिल्यास काय होईल?

\--- /collapse \---