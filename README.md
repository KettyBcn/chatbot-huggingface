# Chatbots with Hugging Face Transformers

Two terminal chatbots built in Python, showing the evolution from classic
Seq2Seq models to modern instruction-tuned LLMs.

## Project structure

- `chatbot.py` — Classic chatbot using **facebook/blenderbot-400M-distill**
  (encoder-decoder / Seq2Seq). The prompt, conversation history and
  formatting are built manually.
- `chatbot_llm.py` — Modern chatbot using **HuggingFaceTB/SmolLM2-360M-Instruct**
  (decoder-only causal LLM). Uses structured messages with roles
  (`system`, `user`, `assistant`) and Hugging Face chat templates.

## What each version demonstrates

| | Part 1 (Seq2Seq) | Part 2 (Causal LLM) |
|---|---|---|
| Model class | `AutoModelForSeq2SeqLM` | `AutoModelForCausalLM` |
| Prompt building | Manual (`User: ... Bot:`) | `apply_chat_template()` |
| History | Plain list of strings | Role-based message list |
| Output | Response only | Prompt + response (sliced) |
| Personality | Fixed by training | Defined via system prompt |

Both versions keep a trimmed conversation history to stay within the
model's token limit, and expose generation parameters (`temperature`,
`top_p`, `repetition_penalty`, `no_repeat_ngram_size`) for tuning
response style.

## How to run

```bash
python -m venv my_env
my_env\Scripts\activate        # Windows
# source my_env/bin/activate   # Linux / macOS

pip install -r requirements.txt

python chatbot.py       # Part 1
python chatbot_llm.py   # Part 2
```

Type `exit` to quit the conversation.

Note: the first run downloads the models from the Hugging Face Hub;
subsequent runs use the local cache. Both models run on CPU.

## Credits

Based on the IBM SkillsBuild / cognitiveclass.ai lab
"Create a simple chatbot with open-source LLMs using Python and Hugging Face"
(Apache 2.0). Code assembled and documented as part of my AI application
development training.
