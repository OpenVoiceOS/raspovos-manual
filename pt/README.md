# Bem-vindo ao OpenVoiceOS e ao seu novo dispositivo raspOVOS

[OpenVoiceOS.org](https://OpenVoiceOS.org)
 
 raspOVOS is a complete, customizable, and open source voice assistant developed to run on a Raspberry Pi.  (Tested with 3b/4/5)
 
 **Github links:**
 [OpenVoiceOS](https://github.com/OpenVoiceOS)
 [raspOVOS](https://github.com/OpenVoiceOS/raspOVOS)
 
 **Matrix chat room**
 [OVOS support](https://matrix.to/#/#OpenVoiceOS-Support:matrix.org)

---

## O que é OVOS e raspOVOS

OVOS (OpenVoiceOS) é uma coleção de pacotes Python que quando reunidos criam um assistente de voz INCRÍVEL e orientado à privacidade, capaz de rodar totalmente no dispositivo ou em uma LAN local. [^1]

raspOVOS is a modified image of [raspberry pi OS](https://www.raspberrypi.com/software/) containing the OVOS software stack.

O raspOVOS é especial por causa de um software especial que permite a detecção automática e configuração de vários dispositivos, incluindo microfones USB, HATs de microfone reSpeaker e outros. [^2]

---

### Primeira inicialização com seu dispositivo raspOVOS

Depending on the version of Pi that is used, determines how fast the first boot will take.  A Pi3b will take SEVERAL minutes to perform the first boot.
 
 If you have a screen attached, you can view the boot process happening.
 The first boot will finish the install process by resizing your disk and enabling all of the OVOS services.
 
 **NOTE** This is a headless device and you will be prompted with a voice on how to proceed with your first setup.
 
 After a few minutes, depending on your device, you will here a voice prompt on how to setup your WiFi.  LAN connections will skip this step.
 
 Expect a prompt such as this.

> "Eu criei uma rede WiFi temporária chamada OVOS. Conecte-se a ela pelo seu telefone ou computador e vá para OpenVoiceOS.com. Escolha a rede WiFi da lista à qual você gostaria de conectar seu dispositivo."


Depois disso, seu dispositivo continuará a configurar o OVOS e as habilidades que exigem acesso à Internet. [^3]

 Agora você deve ter um assistente de voz funcional!!

---

## O que vem depois?

Seu assistente de voz deve estar completo agora, mas você pode fazer muito mais.

### Acesse seu assistente de voz

O raspOVOS vem com um servidor ssh já habilitado, então você poderá acessar seu assistente de qualquer computador conectado à mesma LAN.

 Abra um terminal e digite o seguinte comando.
 `ssh ovos@raspovos`
 Em seguida, ele solicitará a senha.
 `ovos` [^4]

 Ao efetuar login, uma bela arte ASCII (cortesia da [Goldyfruit](https://github.com/goldyfruit) ) será exibida, com algumas ferramentas de linha de comando incluídas no raspOVOS.

---

#### Ferramentas de linha de comando

**[ovos-config](https://github.com/OpenVoiceOS/ovos-config)**

 Uma pequena ferramenta auxiliar está incluída para mostrar, obter ou definir valores de configuração rapidamente

 Resumo rápido (cli):

- `ovos-config get`
- Pesquisa livre (pesquisar uma chave ou partes dela)


Dada uma entrada de

```
    {'PHAL': {
            'ovos-PHAL-plugin-system': {
                    'enabled': True
            },
            'ovos-PHAL-plugin-connectivity-events': {
                    'enabled': True
            },
            ...
    }

`ovos-config get -k phal` would yield  **all**  PHAL entries and present it to the user (and the path where they were found)
```

- Busca restrita (chaves de busca em um local distinto):

    `ovos-config get -k /PHAL/ovos-PHAL-plugin-system/enabled`

    Isso produzirá apenas o valor ou sairá se nenhuma chave for encontrada (barra raiz indicando uma pesquisa estrita)

- `ovos-config set`

    - Pesquisa vagamente por chaves que contenham a sequência de consulta e apresenta uma opção ao usuário para definir um valor

        `ovos-config set -k phal`

        O tipo é derivado da configuração unida e, portanto, pode ser convertido com segurança na configuração do usuário.
         Opcionalmente, um valor ( `-v` ) pode ser enviado como argumento.

- `ovos-config show`

    - Obtenha uma tabela completa da configuração unida, do usuário ( `-u` ), do sistema ( `-s` ) ou remota ( `-r` ).
         Isso pode ser ainda mais refinado passando um `--section` , que pode ser listado com `ovos-config show -l`

**ovos-listen**
 
 `ovos-listen` activates the microphone without using a wakeword. eg "Hey Mycroft"
 Enter `ovos-listen` into the terminal and ask a question with your voice.
 **ovos-speak**
 
 `ovos-speak <phrase>` Have your OVOS device say what you type.
 
 **ovos-say-to**
 
 `ovos-say-to <phrase>`  Send an utterance, command, to your OVOS device as if it was spoken.
 \

### Ver a documentação


 **ovos-docs-viewer**
 
 `ovos-docs-viewer <community/technical/hivemind/messages>`
 
 You can view the OVOS documentation in your terminal.
 \

### Depuração


O OVOS fornece um script auxiliar para visualizar os logs produzidos durante a operação do seu dispositivo.
 [ovos-logs](https://github.com/OpenVoiceOS/ovos-utils/blob/dev/ovos_utils/log_parser.py) pode ajudar a navegar pelos logs. Para uso veja o [ovos-util](https://github.com/OpenVoiceOS/ovos-utils/blob/dev/README.md) README.md

 O raspOVOS também inclui um script para permitir a visualização dos logs em tempo real.
 digite `ologs` em um terminal e os logs serão exibidos. `<ctl>-C` para sair.

Por padrão, o OVOS mostrará apenas os logs marcados como `INFO` . Isso economiza espaço precioso em disco e não tem tanta informação mostrada.

 Isso pode ser alterado através do arquivo de configuração.
 \

### Configuração avançada


O arquivo de configuração do usuário pode ser encontrado em `~/.config/mycroft/mycroft.conf`
 Este é um arquivo JSON padrão e pode ser verificado com o comando `cat ~/.config/mycroft/mycroft.conf | jq` \

### Habilidades


Skills devem ser instaláveis via PIP e devem ser colocadas no raspOVOS venv localizado em `~/.venv` . O venv é ativado automaticamente quando você faz login com um shell.

 Exemplo:
 `pip install ovos-skill-moviemaster`

---

[^1] Pi4/5 para uso completo no dispositivo.
 [^2] Uma lista completa está disponível nos repositórios [ovos-i2csound](https://github.com/OpenVoiceOS/ovos-i2csound) e [ovos-i2c-detection](https://github.com/OpenVoiceOS/ovos-i2c-detection) no GitHub.
 [^3] Todas as habilidades são opcionais, mas algumas exigem uma conexão de internet para funcionar, previsões do tempo para uma. E até mesmo a data/hora por causa da falta de um relógio persistente em um Raspberry Pi.
 [^4] O usuário:senha padrão é `ovos:ovos` . É sugerido que você altere a senha por motivos de segurança. O usuário `ovos` tem privilégios de root e pode alterar seu sistema de arquivos completo sem ser solicitado a fornecer uma senha.
