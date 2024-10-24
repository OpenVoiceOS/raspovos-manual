# Bem-vindo ao OpenVoiceOS e ao seu novo dispositivo raspOVOS

[OpenVoiceOS.org](https://OpenVoiceOS.org)<br><br> raspOVOS é um assistente de voz completo, personalizável e de código aberto desenvolvido para Raspberry Pi. (Testado com 3b/4/5)<br><br> **Links do Github:**<br> [OpenVoiceOS](https://github.com/OpenVoiceOS)<br> [raspOVOS](https://github.com/OpenVoiceOS/raspOVOS)<br><br> **Sala de bate-papo Matrix**<br> [Suporte OVOS](https://matrix.to/#/#OpenVoiceOS-Support:matrix.org)

---

## O que é OVOS e raspOVOS

OVOS (OpenVoiceOS) é uma coleção de pacotes Python que quando reunidos criam um assistente de voz INCRÍVEL e orientado à privacidade, capaz de rodar totalmente no dispositivo ou em uma LAN local. [^1]

raspOVOS é uma imagem modificada do [Raspberry Pi OS](https://www.raspberrypi.com/software/) que contém o software OVOS.

O raspOVOS é especial por causa de um software especial que permite a detecção automática e configuração de vários dispositivos, incluindo microfones USB, HATs de microfone reSpeaker e outros. [^2]

---

### Primeira inicialização com seu dispositivo raspOVOS

Dependendo da versão do Pi que é usada, determina quão rápido o primeiro boot vai ser. Um Pi3b vai demorar VÁRIOS minutos para executar o primeiro boot.<br><br> Se você tiver uma tela anexada, poderá visualizar o processo de inicialização acontecendo.<br> A primeira inicialização finalizará o processo de instalação redimensionando o seu disco e habilitando todos os serviços do OVOS.<br><br> **OBSERVAÇÃO:** Este é um dispositivo sem interface e você receberá uma mensagem de voz sobre como prosseguir com sua primeira configuração.<br><br> Após alguns minutos, dependendo do seu dispositivo, você ouvirá um prompt de voz sobre como configurar o  WiFi. Conexões LAN não tem esta etapa.<br><br> Espere uma mensagem como essa.

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

**ovos-listen**<br><br> `ovos-listen` ativa o microfone sem usar uma palavra de ativação. por exemplo "Hey Mycroft"<br> Digite `ovos-listen` no terminal e faça uma pergunta com sua voz.<br> **ovos-speak**<br><br> `ovos-speak <phrase>` Faça com que seu dispositivo OVOS diga o que você digita.<br><br> **ovos-say-to**<br><br> `ovos-say-to <phrase>` Envie uma declaração, um comando, para seu dispositivo OVOS como se fosse falado.<br> \

### Ver a documentação

<br>**ovos-docs-viewer**<br><br> `ovos-docs-viewer <community/technical/hivemind/messages>`<br><br> Você pode visualizar a documentação do OVOS no seu terminal.<br> \

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
