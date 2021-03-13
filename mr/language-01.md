---
layout: "lesson"
lang: "mr"
title: "मराठी भाषाविशिष्ट सोयी"
description: "मराठी भाषेत लाटेक्-दस्तऐवज बनवताना उपयुक्त ठरतील अशा काही शिफारसी"
next: "extra-01"
toc-anchor-text: "मराठी भाषाविशिष्ट सोयी"
toc-description: "मराठी भाषेत लाटेक्-दस्तऐवज बनवणे."
---

# मराठी भाषाविशिष्ट सोयी
<span class="summary">
  ह्या प्रकरणात मराठी भाषेत लाटेक्-दस्तऐवज बनवताना उपयुक्त ठरतील अशा काही शिफारसी करण्यात
  आल्या आहेत
</span>

## देवनागरी लिपी

मूलतः लाटेक् इंग्लिश वापरकर्त्यांचा विचार करून घडवण्यात आले, त्यामुळे लाटेक्-मध्ये मराठीचा वापर
सुलभ नाही. सर्वात महत्त्वाची अडचण देवनागरी लिपीचा वापर. ASCII अक्षरांचा वापर करणाऱ्या
भाषा लाटेक्-सह सहज वापरता येतात, परंतु ASCII अक्षरांमध्ये देवनागरी लिपीचा समावेश
नाही. देवनागरीकरिता युनिकोड प्रणाली वापरावी लागते. लाटेक्-मध्ये झीलाटेक् व लुआलाटेक् ह्या
चालकांसह युनिकोड अक्षरे वापरता येतात. टेक्-वितरणासह
[शोभिका](https://ctan.org/pkg/shobhika) हा युनिकोड-आधारित टंक येतो. शिवाय
[एकटाईप-टंक](https://ctan.org/pkg/ektype-tanka) हा आज्ञासंच एक-टाईप संस्थेचे काही
युनिकोड-आधारित टंक पुरवतो. लाटेक्-मध्ये मराठी लिहायचे निरनिराळे मार्ग आहेत. सर्वात कमी कष्टात
ते पुढील प्रकारे साधता येऊ शकते. पुढील उदाहरण झीलाटेक् अथवा लुआलाटेक् ह्यांपैकी कोणत्याही
चालकासह चालवता येऊ शकते. लुआलाटेक् हा चालक लुआ आज्ञावलीच्या प्रगत संसाधनांसह वापरता येऊ
शकतो, त्यामुळे मराठीसाठी तो चालक वापरावा अशी शिफारस आम्ही करू.

[मराठी आज्ञासंच](https://ctan.org/pkg/marathi) अनेक भाषाविशिष्ट आज्ञांची पूर्वभरणी करतो
व त्यामुळे मराठीचा लाटेक्-मधील वापर अतिशय सुलभ होतो. हा आज्ञासंच न वापरतादेखील मराठीतून
लाटेक्-अक्षरजुळणी शक्य आहे. [बेबल](https://ctan.org/pkg/babel) व
[पॉलिग्लॉसिया](https://ctan.org/pkg/polyglossia) हे दोन आज्ञासंच लाटेक्-मधील मूलभूत
इंग्रजी शब्दांची भाषांतरे पुरवतात. त्यांचा वापर करून व शोभिका टंक निवडून पुढील दोन प्रकारे अक्षरजुळणी
करता येऊ शकते.

### मराठी आज्ञासंचासह अक्षरजुळणी

```latex
%!TeX lualatex
\documentclass{article}
\usepackage{marathi}

\begin{document}
  नमस्कार!
\end{document}
```

### बेबल आज्ञासंचासह अक्षरजुळणी

```latex
%!TeX lualatex
\documentclass{book}
\usepackage{babel}
\babelprovide[
  import,
  main,
  maparabic, %% मजकुरातील देवनागरी आकडे मिळवण्यासाठी
  mapdigits, %% इतरत्र दिसणाऱ्या इंग्रजी आकड्यांऐवजी देवनागरी आकडे मिळवण्यासाठी
  counters/स्वर = अ आ इ ई उ ऊ ए ऐ ओ औ अं अः ॲ ऋ ऌ ऑ,
  alph=स्वर, %% abcd ह्या लॅटिन व्यंजनांऐवजी देवनागरी व्यंजने मिळवण्यासाठी
  counters/व्यंजन =
  क ख ग घ ङ
  च छ ज झ ञ
  ट ठ ड ढ ण
  त थ द ध न
  प फ ब भ म
  य र ल व श ष स ह ळ,
  Alph=व्यंजन, %% ABCD ह्या लॅटिन व्यंजनांऐवजी देवनागरी व्यंजने दिसण्यासाठी
]
{marathi}
\usepackage{fontspec}
\setmainfont[%
  Language=Marathi, %% भाषाविशिष्ट अक्षरे निवडण्यासाठी. (उदा. हिन्दी श वि. मराठी श)
  Renderer=Harfbuzz, %% जोडाक्षरे व्यवस्थित दिसण्यासाठी
  Script=Devanagari %% जोडाक्षरे व्यवस्थित दिसण्यासाठी
]%
{Mukta} 
%% मुक्तऐवजी कोणताही देवनागरी टंक वापरला जाऊ शकतो, परंतु तो टेक्-वितरणात असायला हवा अथवा
%% तुमच्या संगणकावर असायला हवा.

\begin{document}
नमस्कार!
\end{document}
```

### पॉलिग्लॉसिया आज्ञासंचासह अक्षरजुळणी

```latex
%!TeX xelatex
\documentclass{article}
\usepackage{polyglossia}
\setdefaultlanguage{marathi}
\setmainfont[%
  Language=Marathi, %% भाषाविशिष्ट अक्षरे निवडण्यासाठी. (उदा. हिन्दी श वि. मराठी श)
  Mapping=devanagarinumerals, %% दस्तऐवजात देवनागरी आकडे येण्यासाठी
  Script=Devanagari %% जोडाक्षरे व्यवस्थित दिसण्यासाठी
]%
{Mukta} 
%% मुक्तऐवजी कोणताही देवनागरी टंक वापरला जाऊ शकतो, परंतु तो टेक्-वितरणात असायला हवा अथवा
%% संगणकावर असायला हवा.

\begin{document}
  नमस्कार!
\end{document}
```