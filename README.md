# Automação Médica

Este repositório contém experimentos e protótipos utilizados na automação do consultório da Dra. Alessandra Morais. Os artefatos principais são o servidor web (Raspberry Pi) e o cliente desktop para Windows.

## Cliente Desktop Windows

O cliente Windows foi atualizado para reutilizar diretamente a interface web hospedada no Raspberry Pi. Para isso ele abre um _webview_ leve apontando para `http://pi.local:8080` sempre que o dispositivo está acessível.

### Dependências obrigatórias

1. **Python 3.10+**
2. **[pywebview](https://pywebview.flowrl.com/)**
3. **[Microsoft Edge WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/)** (já vem com o Windows 11, mas inclua o instalador offline no pacote para Windows 10)

Instalação sugerida via `pip`:

```powershell
py -m pip install --upgrade pip
py -m pip install pywebview requests speechrecognition pyautogui pynput
```

Durante o empacotamento com PyInstaller ou similares, garanta que o módulo `pywebview` esteja listado nas dependências e distribua o instalador do WebView2 (`MicrosoftEdgeWebView2RuntimeInstallerX64.exe`) junto com o executável para que o usuário possa instalá-lo antes da primeira execução.

### Comportamento offline

Se o Raspberry Pi não puder ser alcançado, o cliente mostra uma tela simples com instruções para conectar-se à mesma rede e um botão **"Tentar novamente"**. Assim que a conexão for restabelecida, a interface web será carregada automaticamente. Caso o `pywebview` não esteja instalado, a tela avisará o usuário para instalar o pacote e reabrir o aplicativo.

### Execução

```powershell
py ClienteWindows
```

---

Para executar diretamente a interface web sem o cliente desktop, acesse `http://pi.local:8080` a partir de um navegador moderno conectado à mesma rede.
