# Affirm Counter 2.0

## Publicar atualização no GitHub Pages
1. Extraia este ZIP.
2. No repositório `affirm-counter` do GitHub, envie **todos os arquivos** desta pasta para a raiz do repositório (`index.html`, `app.js`, `config.js`, `manifest.webmanifest`, `icon-192.png`, `icon-512.png`). Não envie apenas o ZIP.
3. Confirme o commit. Espere o GitHub Pages atualizar e recarregue o site.
4. O histórico e as afirmações são armazenados no navegador. A versão anterior é importada automaticamente na primeira abertura, considerando o total antigo como repetições do dia da migração (a versão antiga não guardava datas).

## Instalar na tela inicial
- iPhone: abra o link publicado no **Safari** > Compartilhar > Adicionar à Tela de Início. Depois, teste o microfone dentro do ícone instalado; se não funcionar, continue usando no Chrome, onde você já testou.
- Windows: Chrome > menu de três pontos > Transmitir, salvar e compartilhar > Instalar página como app (o nome da opção pode variar).

## Ativar sincronização (opcional)
1. Acesse https://console.firebase.google.com e crie um projeto.
2. Em Authentication > Sign-in method, habilite **Email/Password**.
3. Em Firestore Database, crie um banco (escolha uma região próxima) e abra a aba **Rules**. Substitua pelas regras fornecidas no arquivo `firestore.rules` e publique-as. **Não use regras abertas a qualquer usuário.**
4. Em Project settings > Your apps, adicione um app Web. Copie o objeto `firebaseConfig` fornecido pelo Firebase.
5. No arquivo `config.js`, substitua `null` pelo objeto copiado. Exemplo:

```js
window.AFFIRM_FIREBASE_CONFIG = {
  apiKey: "...",
  authDomain: "seu-projeto.firebaseapp.com",
  projectId: "seu-projeto",
  appId: "..."
};
```

6. Publique o `config.js` atualizado no GitHub. No aplicativo, crie uma conta com e-mail e senha em **um** dispositivo. No outro, entre na mesma conta.
7. Ao entrar pela primeira vez, se ainda não houver dados na nuvem, os dados locais desse dispositivo serão enviados. Nos outros dispositivos, os dados da nuvem terão prioridade. Use **Enviar dados locais para a nuvem** apenas se realmente quiser substituir os dados remotos.

**Importante:** use apenas um dispositivo por vez durante a configuração inicial. Não faça alterações simultâneas nas listas ou metas em dois dispositivos; a última edição pode substituir a anterior. A contagem usa transações na nuvem quando conectado, mas falhas de rede podem impedir o envio de algumas contagens. O app preserva os dados locais, porém não possui uma fila persistente para reenvio automático. Para evitar divergências, utilize conexão estável.

## Limitações
- Reconhecimento de voz é dependente do navegador, pode precisar de internet e pode errar frases repetidas rapidamente.
- O histórico segue a data local de cada aparelho; ajuste relógios/fusos corretamente.
- Sem Firebase, o histórico é local e não é compartilhado entre dispositivos.
- A instalação na tela inicial depende das opções do navegador e do iOS.
