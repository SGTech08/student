---
layout: post
title: Chat GPT Interaction
description: A page to minimistically help you talk with chat GPT
toc: True
comments: False
categories: ['5.A', 'C4.1']
courses: {'csse': {'week': 1}, 'csp': {'week': 3, 'categories': ['6.B']}, 'csa': {'week': 1}}
type: hacks
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat GPT</title>
</head>
<body>
    <h1>ChatGPT</h1>
    <div>
        <span>Question</span>
        <input id="question" type="text" />
        <button onclick="askQuestion()">Ask</button>
    </div>
    <div>
        <span>Answer:</span>
        <p id="answer"></p>
    </div>
    <script>
        async function chatWithGPT(prompt) {
            const API_KEY = "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"; /* your api key here */
            
            const headers = {
                "authorization": `Bearer ${API_KEY}`,
                "content-type": "application/json"
            };

            const data = {
                model: "text-davinci-003",
                prompt: prompt,
                temperature: 1,
                max_tokens: 456,
                top_p: 0.3,
                frequency_penalty: 1.23,
                presence_penalty: 0
            };

            const response = await fetch("https://api.openai.com/v1/completions", {
                method: "POST",
                headers: headers,
                body: JSON.stringify(data)
            });

            const responseData = await response.json();

            if (response.status == 200) {
                return responseData.choices[0].text.trim();
            } else {
                return `Error: ${response.status}, ${responseData.error.message}`;
            }
        }

        async function askQuestion() {
            const question = document.querySelector("#question").value;
            const answerContainer = document.querySelector("#answer");

            answerContainer.textContent = await chatWithGPT(question);
        }
    </script>
</body>
