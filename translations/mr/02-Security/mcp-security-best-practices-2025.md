<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c3f4ea5732d64bf965e8aa2907759709",
  "translation_date": "2025-07-17T01:56:13+00:00",
  "source_file": "02-Security/mcp-security-best-practices-2025.md",
  "language_code": "mr"
}
-->
# MCP सुरक्षा सर्वोत्तम पद्धती - जुलै 2025 अपडेट

## MCP अंमलबजावणीसाठी सर्वसमावेशक सुरक्षा सर्वोत्तम पद्धती

MCP सर्व्हरवर काम करताना, तुमचा डेटा, पायाभूत सुविधा आणि वापरकर्त्यांचे संरक्षण करण्यासाठी खालील सुरक्षा सर्वोत्तम पद्धती पाळा:

1. **इनपुट व्हॅलिडेशन**: इंजेक्शन हल्ले आणि confused deputy समस्या टाळण्यासाठी नेहमी इनपुटची पडताळणी आणि स्वच्छता करा.
   - सर्व टूल पॅरामीटर्ससाठी कडक पडताळणी करा
   - विनंत्या अपेक्षित स्वरूपात आहेत यासाठी स्कीमा व्हॅलिडेशन वापरा
   - प्रक्रिया करण्यापूर्वी संभाव्य धोकादायक सामग्री फिल्टर करा

2. **अॅक्सेस कंट्रोल**: तुमच्या MCP सर्व्हरसाठी योग्य प्रमाणीकरण आणि अधिकृतता लागू करा, ज्यात सूक्ष्म परवानग्या असाव्यात.
   - Microsoft Entra ID सारख्या स्थापित ओळख प्रदात्यांसह OAuth 2.0 वापरा
   - MCP टूल्ससाठी रोल-आधारित अॅक्सेस कंट्रोल (RBAC) लागू करा
   - स्थापित उपाय उपलब्ध असताना कस्टम प्रमाणीकरण कधीही लागू करू नका

3. **सुरक्षित संवाद**: तुमच्या MCP सर्व्हरशी सर्व संवाद HTTPS/TLS वापरून करा आणि संवेदनशील डेटासाठी अतिरिक्त एन्क्रिप्शन विचारात घ्या.
   - शक्य असल्यास TLS 1.3 कॉन्फिगर करा
   - महत्त्वाच्या कनेक्शन्ससाठी सर्टिफिकेट पिनिंग लागू करा
   - सर्टिफिकेट्स नियमितपणे बदलत रहा आणि त्यांची वैधता तपासा

4. **रेट लिमिटिंग**: गैरवापर, DoS हल्ले टाळण्यासाठी आणि संसाधन वापर व्यवस्थापित करण्यासाठी रेट लिमिटिंग लागू करा.
   - अपेक्षित वापराच्या नमुन्यांनुसार योग्य विनंती मर्यादा सेट करा
   - जास्त विनंत्यांवर टप्प्याटप्प्याने प्रतिसाद द्या
   - प्रमाणीकरण स्थितीवर आधारित वापरकर्ता-विशिष्ट रेट लिमिट्स विचारात घ्या

5. **लॉगिंग आणि मॉनिटरिंग**: संशयास्पद क्रियाकलापांसाठी तुमच्या MCP सर्व्हरवर लक्ष ठेवा आणि सर्वसमावेशक ऑडिट ट्रेल्स लागू करा.
   - सर्व प्रमाणीकरण प्रयत्न आणि टूल कॉल्स लॉग करा
   - संशयास्पद नमुन्यांसाठी रिअल-टाइम अलर्टिंग लागू करा
   - लॉग सुरक्षितपणे संग्रहित करा आणि त्यात फेरफार होऊ नये याची खात्री करा

6. **सुरक्षित संचयन**: संवेदनशील डेटा आणि क्रेडेन्शियल्स योग्य एन्क्रिप्शनसह सुरक्षित ठेवा.
   - सर्व रहस्यांसाठी की वॉल्ट्स किंवा सुरक्षित क्रेडेन्शियल स्टोअर्स वापरा
   - संवेदनशील डेटासाठी फील्ड-लेव्हल एन्क्रिप्शन लागू करा
   - एन्क्रिप्शन कीज आणि क्रेडेन्शियल्स नियमितपणे बदलत रहा

7. **टोकन व्यवस्थापन**: सर्व मॉडेल इनपुट्स आणि आउटपुट्सची पडताळणी आणि स्वच्छता करून टोकन पासथ्रू धोके टाळा.
   - ऑडियन्स क्लेम्सवर आधारित टोकन पडताळणी लागू करा
   - तुमच्या MCP सर्व्हरसाठी स्पष्टपणे जारी न केलेले टोकन कधीही स्वीकारू नका
   - योग्य टोकन आयुष्य व्यवस्थापन आणि रोटेशन लागू करा

8. **सेशन व्यवस्थापन**: सेशन हायजॅकिंग आणि फिक्सेशन हल्ले टाळण्यासाठी सुरक्षित सेशन हँडलिंग लागू करा.
   - सुरक्षित, अनिश्चित सेशन आयडी वापरा
   - सेशन्स वापरकर्ता-विशिष्ट माहितीशी बांधा
   - योग्य सेशन कालबाह्यता आणि रोटेशन लागू करा

9. **टूल एक्झिक्युशन सॅंडबॉक्सिंग**: जर तुटले तर साइडवे मोव्हमेंट टाळण्यासाठी टूल एक्झिक्युशन्स वेगळ्या वातावरणात चालवा.
   - टूल एक्झिक्युशन्ससाठी कंटेनर आयसोलेशन लागू करा
   - संसाधन समाप्ती हल्ले टाळण्यासाठी संसाधन मर्यादा लागू करा
   - वेगवेगळ्या सुरक्षा डोमेनसाठी स्वतंत्र एक्झिक्युशन संदर्भ वापरा

10. **नियमित सुरक्षा ऑडिट्स**: तुमच्या MCP अंमलबजावणी आणि अवलंबनांची कालांतराने सुरक्षा पुनरावलोकने करा.
    - नियमित पेनिट्रेशन टेस्टिंग शेड्यूल करा
    - दुर्बलता शोधण्यासाठी स्वयंचलित स्कॅनिंग टूल्स वापरा
    - ज्ञात सुरक्षा समस्या सोडवण्यासाठी अवलंबने अपडेट ठेवा

11. **कंटेंट सेफ्टी फिल्टरिंग**: इनपुट आणि आउटपुट दोन्हीसाठी कंटेंट सेफ्टी फिल्टर्स लागू करा.
    - Azure Content Safety किंवा तत्सम सेवा वापरून हानिकारक सामग्री शोधा
    - प्रॉम्प्ट इंजेक्शन टाळण्यासाठी प्रॉम्प्ट शील्ड तंत्रज्ञान लागू करा
    - तयार केलेल्या सामग्रीत संभाव्य संवेदनशील डेटा लीकिंगसाठी स्कॅन करा

12. **सप्लाय चेन सुरक्षा**: तुमच्या AI सप्लाय चेनमधील सर्व घटकांची अखंडता आणि प्रामाणिकता तपासा.
    - साइन केलेले पॅकेजेस वापरा आणि स्वाक्षऱ्या तपासा
    - सॉफ्टवेअर बिल ऑफ मटेरियल्स (SBOM) विश्लेषण लागू करा
    - अवलंबनांमध्ये हानिकारक अपडेट्ससाठी लक्ष ठेवा

13. **टूल डिफिनिशन संरक्षण**: टूल पॉइझनिंग टाळण्यासाठी टूल डिफिनिशन्स आणि मेटाडेटा सुरक्षित ठेवा.
    - वापरापूर्वी टूल डिफिनिशन्सची पडताळणी करा
    - टूल मेटाडेटामध्ये अनपेक्षित बदलांसाठी लक्ष ठेवा
    - टूल डिफिनिशन्ससाठी अखंडता तपासणी लागू करा

14. **डायनॅमिक एक्झिक्युशन मॉनिटरिंग**: MCP सर्व्हर आणि टूल्सच्या रनटाइम वर्तनावर लक्ष ठेवा.
    - अनोळखी वर्तन ओळखण्यासाठी वर्तनात्मक विश्लेषण लागू करा
    - अनपेक्षित एक्झिक्युशन नमुन्यांसाठी अलर्टिंग सेट करा
    - रनटाइम अ‍ॅप्लिकेशन सेल्फ-प्रोटेक्शन (RASP) तंत्रज्ञान वापरा

15. **किमान विशेषाधिकार तत्त्व**: MCP सर्व्हर आणि टूल्स फक्त आवश्यक किमान परवानग्यांसह कार्य करतील याची खात्री करा.
    - प्रत्येक ऑपरेशनसाठी फक्त विशिष्ट परवानग्या द्या
    - परवानगी वापर नियमितपणे पुनरावलोकन आणि ऑडिट करा
    - प्रशासकीय कार्यांसाठी जस्ट-इन-टाइम अॅक्सेस लागू करा

**अस्वीकरण**:  
हा दस्तऐवज AI अनुवाद सेवा [Co-op Translator](https://github.com/Azure/co-op-translator) वापरून अनुवादित केला आहे. आम्ही अचूकतेसाठी प्रयत्नशील असलो तरी, कृपया लक्षात घ्या की स्वयंचलित अनुवादांमध्ये चुका किंवा अचूकतेची कमतरता असू शकते. मूळ दस्तऐवज त्याच्या स्थानिक भाषेत अधिकृत स्रोत मानला जावा. महत्त्वाच्या माहितीसाठी व्यावसायिक मानवी अनुवाद करण्याची शिफारस केली जाते. या अनुवादाच्या वापरामुळे उद्भवणाऱ्या कोणत्याही गैरसमजुती किंवा चुकीच्या अर्थलागी आम्ही जबाबदार नाही.