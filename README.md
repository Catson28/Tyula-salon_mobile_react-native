This is a new [**React Native**](https://reactnative.dev) project, bootstrapped using [`@react-native-community/cli`](https://github.com/react-native-community/cli).

# Getting Started

>**Note**: Make sure you have completed the [React Native - Environment Setup](https://reactnative.dev/docs/environment-setup) instructions till "Creating a new application" step, before proceeding.

## Step 1: Start the Metro Server

First, you will need to start **Metro**, the JavaScript _bundler_ that ships _with_ React Native.

To start Metro, run the following command from the _root_ of your React Native project:

```bash
# using npm
npm start

# OR using Yarn
yarn start
```

## Step 2: Start your Application

Let Metro Bundler run in its _own_ terminal. Open a _new_ terminal from the _root_ of your React Native project. Run the following command to start your _Android_ or _iOS_ app:

### For Android

```bash
# using npm
npm run android

# OR using Yarn
yarn android
```

### For iOS

```bash
# using npm
npm run ios

# OR using Yarn
yarn ios
```

If everything is set up _correctly_, you should see your new app running in your _Android Emulator_ or _iOS Simulator_ shortly provided you have set up your emulator/simulator correctly.

This is one way to run your app — you can also run it directly from within Android Studio and Xcode respectively.

## Step 3: Modifying your App

Now that you have successfully run the app, let's modify it.

1. Open `App.tsx` in your text editor of choice and edit some lines.
2. For **Android**: Press the <kbd>R</kbd> key twice or select **"Reload"** from the **Developer Menu** (<kbd>Ctrl</kbd> + <kbd>M</kbd> (on Window and Linux) or <kbd>Cmd ⌘</kbd> + <kbd>M</kbd> (on macOS)) to see your changes!

   For **iOS**: Hit <kbd>Cmd ⌘</kbd> + <kbd>R</kbd> in your iOS Simulator to reload the app and see your changes!

## Congratulations! :tada:

You've successfully run and modified your React Native App. :partying_face:

### Now what?

- If you want to add this new React Native code to an existing application, check out the [Integration guide](https://reactnative.dev/docs/integration-with-existing-apps).
- If you're curious to learn more about React Native, check out the [Introduction to React Native](https://reactnative.dev/docs/getting-started).

# Troubleshooting

If you can't get this to work, see the [Troubleshooting](https://reactnative.dev/docs/troubleshooting) page.

# Learn More

To learn more about React Native, take a look at the following resources:

- [React Native Website](https://reactnative.dev) - learn more about React Native.
- [Getting Started](https://reactnative.dev/docs/environment-setup) - an **overview** of React Native and how setup your environment.
- [Learn the Basics](https://reactnative.dev/docs/getting-started) - a **guided tour** of the React Native **basics**.
- [Blog](https://reactnative.dev/blog) - read the latest official React Native **Blog** posts.
- [`@facebook/react-native`](https://github.com/facebook/react-native) - the Open Source; GitHub **repository** for React Native.



#  _____________________________________________________

[![Andres dos Santos](https://media.dev.to/cdn-cgi/image/width=50,height=50,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Fuser%2Fprofile_image%2F482278%2F0365a0b9-779c-472f-8f5f-2e3395497de4.jpeg)](https://dev.to/andresdosantos)

[Andres dos Santos](https://dev.to/andresdosantos)

Posted on 5 de out. de 2020

![img](https://dev.to/assets/sparkle-heart-5f9bee3767e18deb1bb725290cb151c25234768a0e9a2bd39370c382d02920cf.svg)3![img](https://dev.to/assets/multi-unicorn-b44d6f8c23cdd00964192bedc38af3e82463978aa611b4365bd33a0f1f4f3e97.svg)2

# Como criar um projeto React Native com TypeScript

Faaaala Dev's, no meu primeiro post vou ensinar a vocês a como criar um projeto React Native usando o TypeScript, já sabemos que o TS é o "amigo inteligente" do JavaScript, por isso ele vai ser cada vez mais usado no mercado já que as tipagens são de extrema importância na segurança de resposta e na manutenção do código. Já imaginou se o seu código começa a ficar muito grande e daí, no meio do caminho aparece aquele indesejável `undefined`? Isso vai te frustar bastante 😅, mas não se preocupe nós vamos mudando aos poucos tudo para o TypeScript 😎.

Lembrando que não é para *destruirmos o JavaScript de uma vez por todas*, até porque ao final tudo é `bundle`, ou seja, JavaScript.

#### Vamos definir o diretório

Eu particularmente gosto de deixar meus projetos em documentos, então bora navegar até lá.

**No terminal**, garanta que você esteje na raíz do usuário padrão do sistema.

```
$ cd ~
```



Agora que você está no usuário, navegue até `documentos`, para isso vamos usar o `cd` que significa *change directory*.

```
$ cd Documents/
```



Beleza, vamos criar uma pasta para o nosso projeto, usaremos o `mkdir` que significa *make directory*.

```
$ mkdir app
```



### ⚠️Atenção aqui!⚠️

De acordo com as últimas recomendações do pessoal do React não é legal ter o **React Native CLI** instalada globalmente no sistema, então vamos removê-los.

** Desinstalar **

```
$ npm uninstall -g react-native-cli

  ou

$ yarn remove -g react-native-cli
```



```
 npx react-native init MeuPrimeiroApp2024 --template react-native-template-typescript
```



**Finalmente** podemos usar a **cli** do **React Native** para criar um projeto usando **TypeScript**. Então bora lá ...

```
$ npx react-native init FirstAppWithReactNativeAndTS --template react-native-template-typescript 
```