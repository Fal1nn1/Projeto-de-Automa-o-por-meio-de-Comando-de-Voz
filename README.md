# Projeto-de-Automa-o-por-meio-de-Comando-de-Voz

import speech_recognition as sr
import os

# Função para reconhecimento de voz
def reconhecimento_voz():
    # Inicializa o reconhecedor
    reconhecedor = sr.Recognizer()

    with sr.Microphone() as source:
        print("Diga algo...")
        
        # Ajusta para o ruído ambiente
        reconhecedor.adjust_for_ambient_noise(source)
        
        # Escuta o áudio do microfone
        audio = reconhecedor.listen(source)

    try:
        # Reconhece o áudio usando a API do Google
        texto = reconhecedor.recognize_google(audio, language='pt-BR')
        print("Você disse: ", texto)
        return texto.lower()
    except sr.UnknownValueError:
        print("Não foi possível entender o áudio")
        return ""
    except sr.RequestError as e:
        print("Erro ao solicitar resultados; {0}".format(e))
        return ""

# Função para abrir aplicativos com base no comando de voz
def abrir_aplicativo(comando):
    if "excel" in comando:
        os.system("start excel")
    elif "navegador" in comando:
        os.system("start chrome")
    elif "word" in comando:
        os.system("start winword")
    elif "powerpoint" in comando:
        os.system("start powerpnt")
    else:
        print("Aplicativo não reconhecido")

# Função principal
def main():
    print("Bem-vindo ao sistema de automação por reconhecimento de voz!")
    print("Você pode dizer 'sair' a qualquer momento para encerrar o programa.")
    print("--------------------------------------------------------")

    while True:
        comando = reconhecimento_voz()

        if "sair" in comando:
            print("Encerrando o programa...")
            break

        abrir_aplicativo(comando)

if __name__ == "__main__":
    main()

