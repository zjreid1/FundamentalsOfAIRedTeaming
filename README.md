# FundamentalsOfAIRedTeaming

Covering AI Red Teaming 101 – Full Course from Microsoft

- Course: https://www.youtube.com/watch?v=DwFVhFdD2fs
- Associated Labs: https://github.com/microsoft/AI-Red-Teaming-Playground-Labs
- PyRIT (Framework to ID AI risks): https://github.com/Azure/PyRIT


### Key takeaways:

- Understanding how Gen AI models work and where/how to attack them
- Being able to use direct/indirect prompts
- Using multiple prompts to attack via crescendo/skeleton key attacks
- How to defend against attacks w/ delimiters, data marking, and encoding
- Automating attacks w/ the PyRIT Python Framework


### Useful papers/blog posts:

- https://www.microsoft.com/en-us/security/blog/2024/04/11/how-microsoft-discovers-and-mitigates-evolving-attacks-against-ai-guardrails/
- https://www.microsoft.com/en-us/security/blog/2024/06/26/mitigating-skeleton-key-a-new-type-of-generative-ai-jailbreak-technique/
- https://www.microsoft.com/en-us/research/publication/defending-against-indirect-prompt-injection-attacks-with-spotlighting/


### Episdoe 1: What is Red Teaming

<img width="1282" height="683" alt="image" src="https://github.com/user-attachments/assets/1a5e37b0-0c0c-4bbe-b3d6-d15f72b46f09" />

<img width="895" height="596" alt="image" src="https://github.com/user-attachments/assets/a3c144f5-b7c1-467b-ab8c-afa6cd1b9600" />




### Episode 2: How Gen AI Models Work

- Generative AI trained on patters to produce new content differs from traiditional ML which classifies, detects, and predicts
- Multiple Types of training
-   1: Pre-training: Trained on large/diverse datasets (books, code, unsupervised, in multiple languages)
-   2: After pre-training: Safety/instruction post-training is done to align the model based on human feedback
-   3: Brak/fix cycle: Measure + AI red teams to align model to RAI policies
-   4: Additional Guardrails: More guardrails added to reduce harmful/inappropraite outputs

- Token: chunk of text/punctuation/whole words, etc...
- If you understand how the Model is ingesting/reading tokens you can start to sneak things past it to bypass guardrails
- Each token is turned into a vector which weights each word/phrase and how it relates to other words/phrases.  Transformation models picks up on contexts within long strings of tokens/text/input

### Episode 3: Direct Prompt Injection Explained

AI Prompt injection example

1:  Example application of AI (email summarization bot)
<img width="1282" height="732" alt="image" src="https://github.com/user-attachments/assets/7cf74b18-104a-4081-bd73-83f51f616568" />

2:  Direct prompt injection attack
<img width="1292" height="653" alt="image" src="https://github.com/user-attachments/assets/dc9a5dda-7d1d-49bb-82cd-905195589f7c" />


- Context window: The full stream/sequence of tokens that provides the conditions for what it is supposed to carry out
- If an attacker can influence/override the input, an attacker can retrieve/manipulate data

Case Study:
- Car dealership in Quebec implemented a chatbot and repeatedly attempted to sell cars for $1.00, an example of what can happen if input isn't constrained

<img width="820" height="440" alt="image" src="https://github.com/user-attachments/assets/97f17c56-4f3d-4c3f-8e2f-26c3001d7ae0" />

### Episode 4: Indirect Prompt Injection

1:  Example application of AI (email summarization bot)
<img width="1282" height="732" alt="image" src="https://github.com/user-attachments/assets/7cf74b18-104a-4081-bd73-83f51f616568" />

2: Model of indirect prompt injection
<img width="1283" height="652" alt="image" src="https://github.com/user-attachments/assets/3d4d2200-fd84-4987-b908-054dcfc272a7" />

- Direct prompt injection: We directly ask the LLM to do something and posion the input

- With  indirect attack injection we are trying to poison the  data source to be able to use it to poison the model 

  - Direct injection: Send all email summarizations to a malicious external email
  - Indirect injection: Summarize emails (email contains instructions to send emails to a malicious external email)



Indirect Attack example:
<img width="1198" height="620" alt="image" src="https://github.com/user-attachments/assets/d84c5784-44ab-41eb-a443-59593e105719" />

Episode 5: Prompt Injection Attacks

- Single turn attacks: Single prompt crafted to make the model misbehave/reveal information

Model of Single turn attack:
<img width="1292" height="732" alt="image" src="https://github.com/user-attachments/assets/182c7982-76cc-4eaf-89d9-1479f5934a88" />

- It is possible to socially engineer LLMs
  - Emotional Appeal (Threatening/gashlighting/encouragement)
  - Narrative/Role Play (storytelling: i.e. I'm writing a thriller or I'm an Incident Responder)
  - Technical context tricks (Give it malicious examples, behavior priming (always start the answer with yes)

 - Various obfuscation techniques to bypass guardrails such as string matching filters
<img width="915" height="605" alt="image" src="https://github.com/user-attachments/assets/fa0d942b-b76f-43f2-91da-5a96fafa4149" />


### Episode 6: Prompt Injection Attacks 2

- Different types of attacks that use prompts over time or multiple steps to gain access

A: Skeleton Key attacks: https://www.microsoft.com/en-us/security/blog/2024/06/26/mitigating-skeleton-key-a-new-type-of-generative-ai-jailbreak-technique/

- User prompt that puts the model in a mode where a user can directly request information

Skeleton Key Attack Model

<img width="916" height="640" alt="image" src="https://github.com/user-attachments/assets/dfe5b087-0633-4d3a-b22b-e14288562393" />



B: Crescendo attacks: https://www.microsoft.com/en-us/security/blog/2024/04/11/how-microsoft-discovers-and-mitigates-evolving-attacks-against-ai-guardrails/

- Start with harmless user prompts that incrementally work the model towards harmful output

Crescendo attack example:

<img width="862" height="611" alt="image" src="https://github.com/user-attachments/assets/00bc035f-caa4-46e7-85ca-a8d91fa40c56" />




### Episode 7: Defending Against Attacks

Spotlighting: https://www.microsoft.com/en-us/research/publication/defending-against-indirect-prompt-injection-attacks-with-spotlighting/

- Family of prompt engineering techniques to improve LLMs ability to distinguish between trusted vs untrusted input sources, with specific sub-techniques

- Delimiting: Special tokens are prepended/appended

Deliminting example:

<img width="1272" height="695" alt="image" src="https://github.com/user-attachments/assets/189fa765-97f1-45da-ad86-dfbe980fd400" />


- Data Marking: Delimiting extension by interleaving a special token through the entire text

Data Marking Example

<img width="1258" height="712" alt="image" src="https://github.com/user-attachments/assets/d61d73f4-3109-4d97-8ab6-a6f0d3b53d35" />


- Encoding: Text transformed to make the input obvious to the model

Encoding example:

<img width="1240" height="691" alt="image" src="https://github.com/user-attachments/assets/dc63e2d5-9212-4e13-bc2e-be01e7bb887d" />



### Episode 8: Automating AI Red Teaming w/ PyRIT

- AI Red Teaming Tool created by MS that is open source to assist researchers to evaluate AI systems in an automated manner
- Primary use cases are for red teams, efficency gains for red team workflows, increased relaibility, and for flexibility for various application needs

PyRIT Architecture:

<img width="905" height="590" alt="image" src="https://github.com/user-attachments/assets/230afaba-4b31-4114-83ba-c082512f20c8" />

PyRIT example workflow:

<img width="1225" height="613" alt="image" src="https://github.com/user-attachments/assets/c2f2450b-5384-4ae5-b8f9-4b295aeba1bc" />



### Episode 9: Automating Prompt injection Attacks w/ PyRIT

- Can set a number of variables, scores, prompts, and attempts within PyRIT along with different ways to "score" the output based on success/failure depending on a number of contexts/dispositions

### Episode 10: Automating Multi Turn attacks w/ PyRIT

- Can use Red Teaming orchestrator which basically pits 2 LLMs against each other for a specified number of tries given a number of variables such as with single turn/direct prompt injection.
