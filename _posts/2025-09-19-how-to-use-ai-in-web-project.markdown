---
date: "2025-09-19 08:08:12 +0545"
layout: post
title: "VS Code मार्फत वेब प्रोजेक्टमा ChatGPT, Claude र Deepseek AI कसरी प्रयोग गर्ने?"
---

AI अब coding मात्र होइन, software development workflow को अनिवार्य हिस्सा बन्दै गएको छ। OpenAI को ChatGPT, Anthropic को Claude, र Deepseek जस्ता LLM (Large Language Models) ले डेभलपरको प्रोडक्टिभिटी कयौ गुणा बढाइरहेका छन्। यसको प्रयोग शुरु गरी नसकेकाहरुको मनमा प्रश्न उठ्न सक्छ  VS Code मा यी AI कसरी जोड्ने? Subscription भन्दा API किन सस्तो हुन्छ? आफ्नो प्रोजेक्ट वा working directory भित्र कसरी integrate गर्ने?
यो लेखमा हामी step-by-step हेर्नेछौं: Installation → Integration → Prompt Engineering → Cost Management बारेमा कुरा गर्छौ । 

Visual Studio Code सबैभन्दा लोकप्रिय code editor हो, र यसमा AI ईन्ट्रीग्रेट गर्दा फाईदा धेरै छन्। Coding गर्दा हुने repetitive काम घट्छ, boilerplate code तुरुन्त generate हुन्छ, error debugging सजिलो हुन्छ, लामो वा अस्तव्यस्त code लाई refactor गरेर readable बनाउन सकिन्छ, documentation स्वतः generate हुन्छ, र नयाँ framework वा library सिक्दा AI बाट live help पनि पाइन्छ। सरल शब्दमा भन्नुपर्दा, AI VS Code ईन्ट्रीग्रेट गर्दा तपाईँले pair-programmer जस्तै support पाउनुहुन्छ।

यसको लागि सुरुमा केही कुरा आवश्यक हुन्छ। पहिलो भनेको VS Code नै हो , जुन आधिकारिक वेबसाइटबाट डाउनलोड गर्न सकिन्छ। त्यसपछि, तपाईँलाई AI provider को API Key चाहिन्छ — ChatGPT को लागि OpenAI बाट, Claude को लागि Anthropic बाट, र Deepseek को लागि Deepseek platform बाट। अन VS Code मा AI plugin वा extension install गर्नुपर्छ। अहिले प्रचलित extension हरुमा Continue, CodeGPT र ChatGPT – EasyCode पर्छन्, जुन VS Code Marketplace बाट सजिलै उपलब्ध छन्।

अहिले धेरैले ChatGPT Plus वा Claude Pro जस्ता subscription लिएका हुन्छन्, तर subscription र API बीचमा cost फरक हुन्छ। Subscription मा मासिक फिक्स शुल्क हुन्छ, जस्तै ChatGPT Plus को लागि $20 प्रति महिना। तर API मा pay-as-you-go हुन्छ, जसमा प्रयोगअनुसार मात्र बिल आउँछ। उदाहरणका लागि, GPT-4o-mini API लगभग $0.60 प्रति १M tokens पर्छ भने Claude 3.5 Sonnet लगभग $3 प्रति १M tokens पर्छ। Deepseek अझै किफायती दरमा उपलब्ध हुन्छ। त्यसैले heavy user का लागि subscription सजिलो हुन्छ भने selective वा casual प्रयोगकर्ताका लागि API नै धेरै सस्तो विकल्प हो।

Extension install गर्ने प्रक्रिया पनि सजिलो छ। VS Code खोलेर Extensions प्यानल (Ctrl+Shift+X) मा जानुपर्छ र "Continue" वा "CodeGPT" खोजेर install गर्नुपर्छ। Extension install भएपछि Command Palette (Ctrl+Shift+P) खोलेर "Set API Key" मा आफ्नो key राख्न सकिन्छ। चाहिने खण्डमा settings.json फाइलमा पनि API key राख्न सकिन्छ। त्यसपछि editor भित्रै AI panel प्रयोग गर्न सकिन्छ।

अब कुरा गरौँ आफ्नो working directory वा प्रोजेक्टमा AI integrate गर्ने बारेमा। मानौँ तपाईँ CodeIgniter 4 र Tailwind CSS प्रोजेक्टमा AI जोड्न चाहनुहुन्छ भने backend मा एउटा helper library बनाउन सकिन्छ, जसले OpenAI API सँग request पठाएर response ल्याउँछ। त्यसको लागि cURL प्रयोग गरेर https://api.openai.com/v1/chat/completions endpoint मा request पठाउने र user prompt अनुसार response फर्काउने व्यवस्था गर्न सकिन्छ। Controller बाट सो library call गरेर response frontend (React, Vue वा Tailwind UI) मा देखाउन सकिन्छ। यसरी AI feature project को working directory भित्र integrate हुन्छ।


Working Directory / Project मा Integration

यहाँ एउटा साधारण तर practical उदाहरण छ — CodeIgniter 4 + Tailwind प्रोजेक्टमा backend बाट OpenAI call गर्ने तरिका।

Step 1: Helper Library (app/Libraries/OpenAI.php)

```php
<?php
namespace App\Libraries;

class OpenAI {
    private $apiKey;

    public function __construct() {
        $this->apiKey = getenv('OPENAI_API_KEY');
    }

    public function ask($prompt) {
        $ch = curl_init("https://api.openai.com/v1/chat/completions");
        curl_setopt($ch, CURLOPT_HTTPHEADER, [
            "Authorization: Bearer " . $this->apiKey,
            "Content-Type: application/json",
        ]);

        $data = [
            "model" => "gpt-4o-mini",
            "messages" => [
                ["role" => "user", "content" => $prompt]
            ],
        ];

        curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

        $response = curl_exec($ch);
        curl_close($ch);

        return json_decode($response, true);
    }
}
```

Step 2: Controller बाट Call गर्ने उदाहरण

$ai = new \App\Libraries\OpenAI();
$response = $ai->ask("Explain CodeIgniter 4 validation in Nepali");
echo $response['choices'][0]['message']['content'];


यो pattern ले backend मा सुरक्षित तरिकाले API key प्रयोग गर्छ, response JSON मा फर्काउँछ, र frontend (React/Vue/Tailwind UI वा साधारण view) मा देखाउन सजिलो बनाउँछ।

### Prompt Engineering — राम्रो Prompt लेख्ने कला

AI बाट प्रभावकारी नतीजा निकाल्न prompt नै सबैभन्दा महत्वपूर्ण हुन्छ। राम्रो prompt सामान्यतः Context + Instruction + Desired Output Format हुन्छ। केहि प्रयोगी example हरु:

## Bug Fixing

Here is my error: [paste error]
Here is my code: [paste code]
Fix the issue and explain what was wrong.


## Refactoring

Refactor the following PHP code to be cleaner, more secure, and follow best practices. Add comments in Nepali.
[paste code]


## Documentation

Generate detailed documentation in Nepali for this CodeIgniter 4 controller:
[paste controller code]


## Learning

Teach me CodeIgniter 4 sessions step by step in Nepali, with simple examples.


### Pro Tip: role-play गराएर AI लाई context दिनुहोस्, जस्तै:

Act as a senior CodeIgniter 4 developer. Review my code and suggest performance improvements.

API Key सुरक्षित राख्ने तरिका

API key कहिल्यै frontend मा नहाल्नुहोस्।

Development/Production मा .env फाइल वा environment variables प्रयोग गर्नुहोस्।

Cloud मा deploy गर्दा AWS Secrets Manager, GCP Secret Manager वा Azure Key Vault जस्ता services प्रयोग गरेर सुरक्षित राख्नुहोस्।

ध्यान दिनुहोस्: API key leak भएमा अनावश्यक बिल र सुरक्षा जोखिम आउन सक्छ।

निष्कर्ष

VS Code मा ChatGPT, Claude वा Deepseek API जोड्दा coding workflow धेरै productive हुन्छ। Subscription भन्दा API cost-efficient हुन्छ, विशेषगरी कम प्रयोगकर्ताका लागि। Extension install गरेर editor भित्रै AI प्रयोग गर्न सकिन्छ, अनि project वा working directory मा integrate गरेर आफ्नै custom AI features बनाउन सकिन्छ। सबैभन्दा महत्त्वपूर्ण कुरा भनेको राम्रो prompt लेख्ने र API key सुरक्षित राख्ने हो। सुरु गर्न सजिलो छ — VS Code डाउनलोड गर्नुहोस्, Extension install गर्नुहोस्, API Key सेट गर्नुहोस्, र AI लाई आफ्नो coding workflow मा pair-programmer जस्तै प्रयोग गर्न सुरु गर्नुहोस्।
