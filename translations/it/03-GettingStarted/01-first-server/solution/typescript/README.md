<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "ac67652abc453e2a7e2c75cd7a8897ae",
  "translation_date": "2025-07-13T18:05:13+00:00",
  "source_file": "03-GettingStarted/01-first-server/solution/typescript/README.md",
  "language_code": "it"
}
-->
# Esecuzione di questo esempio

Si consiglia di installare `uv` ma non è obbligatorio, vedi [istruzioni](https://docs.astral.sh/uv/#highlights)

## -1- Installa le dipendenze

```bash
npm install
```

## -3- Esegui l'esempio


```bash
npm run build
```

## -4- Testa l'esempio

Con il server in esecuzione in un terminale, apri un altro terminale ed esegui il seguente comando:

```bash
npm run inspector
```

Questo dovrebbe avviare un server web con un'interfaccia visiva che ti permette di testare l'esempio.

Una volta connesso il server:

- prova a elencare gli strumenti ed esegui `add`, con argomenti 2 e 4, dovresti vedere 6 come risultato.
- vai su resources e resource template e chiama "greeting", digita un nome e dovresti vedere un saluto con il nome che hai inserito.

### Test in modalità CLI

L'inspector che hai avviato è in realtà un'app Node.js e `mcp dev` è un wrapper intorno ad essa.

Puoi avviarlo direttamente in modalità CLI eseguendo il seguente comando:

```bash
npx @modelcontextprotocol/inspector --cli node ./build/index.js --method tools/list
```

Questo elencherà tutti gli strumenti disponibili nel server. Dovresti vedere il seguente output:

```text
{
  "tools": [
    {
      "name": "add",
      "description": "Add two numbers",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "title": "A",
            "type": "integer"
          },
          "b": {
            "title": "B",
            "type": "integer"
          }
        },
        "required": [
          "a",
          "b"
        ],
        "title": "addArguments"
      }
    }
  ]
}
```

Per invocare uno strumento digita:

```bash
nnpx @modelcontextprotocol/inspector --cli node ./build/index.js --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Dovresti vedere il seguente output:

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> ![!TIP]
> Di solito è molto più veloce eseguire l'inspector in modalità CLI che nel browser.
> Leggi di più sull'inspector [qui](https://github.com/modelcontextprotocol/inspector).

**Disclaimer**:  
Questo documento è stato tradotto utilizzando il servizio di traduzione automatica [Co-op Translator](https://github.com/Azure/co-op-translator). Pur impegnandoci per garantire accuratezza, si prega di notare che le traduzioni automatiche possono contenere errori o imprecisioni. Il documento originale nella sua lingua nativa deve essere considerato la fonte autorevole. Per informazioni critiche, si raccomanda una traduzione professionale effettuata da un umano. Non ci assumiamo alcuna responsabilità per eventuali malintesi o interpretazioni errate derivanti dall’uso di questa traduzione.