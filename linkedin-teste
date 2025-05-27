import streamlit as st
import openai
import os

# Configuração da chave da OpenAI
openai.api_key = os.getenv("OPENAI_API_KEY")

st.title("🧑‍💼 Persona Content Generator para LinkedIn")

st.sidebar.header("Dados do Executivo")

name = st.sidebar.text_input("Nome")
role = st.sidebar.text_input("Cargo")
sector = st.sidebar.text_input("Setor")

style = st.sidebar.selectbox("Estilo de Comunicação", 
                             ["Inspirador", "Analítico", "Provocador", "Storytelling", "Empático"])

keywords = st.sidebar.text_area("Palavras-chave")
typical_phrases = st.sidebar.text_area("Frases típicas")

st.sidebar.header("Configurações do Conteúdo")

topic = st.sidebar.text_input("Tema central")
goal = st.sidebar.selectbox("Objetivo", 
                            ["Reforçar autoridade", "Criar engajamento", "Promover evento", "Outro"])

references = st.sidebar.text_area("Referências (links ou textos)")
format_type = st.sidebar.selectbox("Formato", 
                                   ["Post curto", "Artigo longo", "Comentário", "Mensagem direta"])

formality = st.sidebar.slider("Grau de formalidade", 0, 100, 50)
emotion = st.sidebar.slider("Tom emocional", 0, 100, 50)

cta = st.sidebar.text_input("Call to Action")

generate_button = st.sidebar.button("Gerar Conteúdo")

if generate_button:
    prompt = f"""
Você é um assistente de marketing especializado em personal branding para executivos.

**Sobre o Executivo:**
- Nome: {name}
- Cargo: {role}
- Setor: {sector}
- Estilo de comunicação: {style}
- Palavras-chave: {keywords}
- Frases típicas: {typical_phrases}

**Sobre o Conteúdo:**
- Tema central: {topic}
- Objetivo: {goal}
- Referências: {references}
- Formato: {format_type}
- Call to Action: {cta}

**Preferências de estilo:**
- Grau de formalidade: {formality}
- Tom emocional: {emotion}

Instruções:
1. Use o tom de voz alinhado ao estilo de comunicação do executivo.
2. Gere 3 variações de conteúdo para LinkedIn.
"""

    with st.spinner("Gerando conteúdo..."):
        response = openai.ChatCompletion.create(
            model="gpt-4-turbo",
            messages=[{"role": "user", "content": prompt}],
            temperature=0.7,
            max_tokens=1500
        )

        result = response.choices[0].message.content

    st.subheader("✅ Conteúdo Gerado")
    st.write(result)
