# 📱 Guia Completo: Gerando APK no React Native

## 📖 Sumário

1. [O que é um APK](#1-o-que-é-um-apk)
2. [O que é preciso saber antes de gerar um APK](#2-o-que-é-preciso-saber-antes-de-gerar-um-apk)
3. [Dois caminhos para gerar um APK](#3-dois-caminhos-para-gerar-um-apk)
   - [3.1 Gerando um APK no React Native CLI](#31-gerando-um-apk-no-react-native-cli)
   - [3.2 Gerando um APK com Expo](#32-gerando-um-apk-com-expo)
4. [Cenários no React Native: Expo vs React Native CLI](#4-cenários-no-react-native-expo-vs-react-native-cli)

---

## 1 O que é um APK

Um APK (Android Package Kit) é o formato de arquivo usado pelo sistema operacional Android para distribuir e instalar aplicativos. Ele contém todos os componentes de um app — código compilado, recursos (imagens, layouts, sons), arquivos de configuração e permissões — necessários para que o aplicativo funcione no dispositivo.

Simplificando, é o "pacote" que o Android precisa para instalar e executar um aplicativo. Quando você baixa um app da Google Play Store, o que realmente está sendo instalado no seu celular é um APK, mesmo que o usuário não veja o arquivo diretamente.

[Voltar ao sumário](#-sumário)

---

## 2 O que é preciso saber antes de gerar um APK

Antes de gerar um APK em React Native, é importante entender alguns cenários para escolher o método certo. Neste guia, o foco é exclusivamente no React Native, mas também daremos um panorama geral do sistema Android. Esse conhecimento ajuda não só a gerar um APK, mas também a lidar com problemas futuros — é melhor entender o que está acontecendo do que depender apenas do Copilot para resolver tudo.

Tradicionalmente, aplicativos Android são criados em linguagens como Java ou Kotlin, que interagem diretamente com o sistema operacional. Esse caminho oferece total controle sobre os recursos do dispositivo e é o padrão da indústria para desenvolvimento nativo.

O React Native permite criar apps para Android e iOS usando um único código-base em JavaScript/TypeScript, aproveitando componentes nativos sob o capô. Isso reduz o tempo de desenvolvimento, o esforço da equipe e os custos de manutenção.

Embora existam diferentes maneiras de gerar um APK usando Java ou Kotlin, neste guia vamos nos concentrar nos métodos disponíveis no contexto do React Native.

[Voltar ao sumário](#-sumário)

---

## 3 Dois caminhos para gerar um APK

No React Native, existem dois cenários principais para gerar um APK: React Native CLI e Expo.

O React Native CLI dá acesso direto ao projeto Android e usa as ferramentas do próprio sistema (como o Gradle e o Android Studio) para compilar o app.

O Expo abstrai parte dessa complexidade e oferece ferramentas próprias para gerar o APK de forma simplificada.

Abaixo, mostramos os dois caminhos separadamente, para que você escolha aquele que corresponde ao tipo de projeto que você tem em mãos.

[Voltar ao sumário](#-sumário)

### 3.1 Gerando um APK no React Native CLI

Se o seu projeto foi criado usando o React Native CLI, você tem acesso direto ao código nativo Android. Isso significa que a geração do APK será feita utilizando o Gradle, a ferramenta de build oficial do Android.

#### 3.1.1 Instalando e configurando o Android Studio

Baixe o Android Studio no site oficial: [developer.android.com/studio](https://developer.android.com/studio)

Durante a instalação, marque a opção para incluir o Android SDK e o Android Virtual Device (AVD). O SDK permite compilar apps, e o AVD cria emuladores para testes.

Abra o Android Studio e vá em:

```
More Actions → SDK Manager
```

Certifique-se de que a versão do SDK corresponde ao compileSdkVersion do seu projeto (geralmente a mais recente).

#### 3.1.2 Configurando variáveis de ambiente (Linux/macOS)

Para que seu terminal encontre o SDK e o Java:

Descubra onde o SDK foi instalado (normalmente ~/Android/Sdk).

Abra o arquivo de configuração do terminal:

```bash
# Bash
nano ~/.bashrc

# Zsh
nano ~/.zshrc
```

Adicione estas linhas ao final do arquivo (ajuste os caminhos se necessário):

```bash
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$ANDROID_HOME/emulator:$ANDROID_HOME/platform-tools:$PATH
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

- `ANDROID_HOME` → indica onde está o SDK do Android
- `PATH` → adiciona comandos do Android (como adb) ao terminal
- `JAVA_HOME` → indica onde está o Java JDK 11

Atualize o terminal:

```bash
source ~/.bashrc   # ou source ~/.zshrc
```

Teste se funcionou:

```bash
java -version
adb --version
```

Se ambos responderem corretamente, seu ambiente está pronto.

#### 3.1.3 Acessando a pasta Android do projeto

No terminal, vá para a pasta android do seu projeto:

```bash
cd android
```

#### 3.1.4 Gerando o APK

Existem duas opções principais:

##### 3.1.4.1 Debug APK

Usado durante o desenvolvimento.

Mais rápido de gerar, contém logs e ferramentas de depuração.

Ideal para testar no seu próprio dispositivo.

```bash
./gradlew assembleDebug
```

O arquivo será criado em:

```
android/app/build/outputs/apk/debug/app-debug.apk
```

##### 3.1.4.2 Release APK

Usado para distribuição e publicação em lojas (Google Play).

Otimizado, mais leve e sem ferramentas de depuração.

```bash
./gradlew assembleRelease
```

O arquivo ficará em:

```
android/app/build/outputs/apk/release/app-release.apk
```

Em resumo: Debug é para testar, Release é para usuários finais.

[Voltar ao sumário](#-sumário)

### 3.2 Gerando um APK com Expo

O Expo simplifica bastante a criação de apps React Native. Com ele, você consegue gerar um APK sem precisar instalar Android Studio ou mexer com Gradle.

#### 3.2.1 Preparando o projeto

Certifique-se de que o projeto está usando Expo (verifique o arquivo app.json e a pasta node_modules/expo).

Instale o Expo CLI globalmente, se ainda não tiver:

```bash
npm install -g expo-cli
```

Faça login na sua conta Expo:

```bash
expo login
```

Se não tiver conta, você pode criar uma aqui no site do [Expo](https://expo.dev/).

#### 3.2.2 Gerando o APK

Expo oferece duas principais opções de APK:

##### 3.2.2.1 APK de teste (development build)

Usado para testar seu app no dispositivo antes de publicar.

Inclui ferramentas de depuração e não é otimizado.

```bash
expo run:android
```

Esse comando instala o app direto no dispositivo conectado ou no emulador.

##### 3.2.2.2 APK de produção (release build)

Usado para distribuição ou publicação em lojas como Google Play.

Otimizado e sem ferramentas de depuração.

```bash
eas build --platform android
```

O EAS Build é um serviço do Expo que compila seu APK nos servidores deles. Isso significa que você não precisa configurar nada no seu computador: o serviço gera o arquivo de release, assina digitalmente e prepara o APK pronto para instalar ou publicar.

[Voltar ao sumário](#-sumário)

---

## 4 Cenários no React Native: Expo vs React Native CLI

Para unificar, podemos resumir os quatro cenários principais:

- **Expo Managed Workflow**

  - Você não mexe com código nativo
  - APK gerado usando `eas build`

- **Expo Bare Workflow**

  - Acesso ao código nativo, mas ainda usa algumas ferramentas do Expo
  - APK gerado com Gradle, dentro do Android Studio, parecido com React Native CLI

- **React Native CLI (Android)**

  - Acesso completo ao código nativo
  - APK gerado manualmente via Gradle

- **React Native CLI (iOS)**
  - Acesso completo ao código nativo para iOS
  - Não gera APK, mas gera arquivos .ipa para publicação na App Store

Em resumo: se seu projeto foi iniciado com Expo Managed, use `eas build`. Se está no Bare Workflow ou no React Native CLI, a geração será feita manualmente via Gradle.

[Voltar ao sumário](#-sumário)
