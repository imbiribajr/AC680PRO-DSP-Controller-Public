# AC680PRO DSP Controller

O **AC680PRO DSP Controller** e um sistema de controle para processadores de audio digitais baseados em **ESP32-CYD** integrado ao **ADAU1452**, com interface moderna em desktop/web, comunicacao Wi-Fi ou serial, controle em tempo real de parametros DSP e visualizacao de niveis de audio.

O projeto combina firmware ESP-IDF, export SigmaStudio e frontend React/Electron em uma solucao unica para controle, calibracao e operacao de audio multicanal.

## Recursos principais

- Controle completo via interface grafica.
- Comunicacao com o DSP por **Wi-Fi/WebSocket** ou **Serial**.
- Matriz de roteamento **6 entradas x 8 saidas**.
- Controle de ganho individual de entradas e saidas com ajuste fracionario.
- Mute e inversao de fase.
- EQ grafico/parametrico de entrada com ate **31 bandas**.
- EQ de saida com **7 bandas**.
- Crossover por canal de saida.
- Limiter por canal de saida com indicacao visual de atuacao.
- Delay de saida em canais suportados.
- VUs digitais em LED e VUs analogicos calibrados.
- Supervisor visual com widgets, conexoes e monitoramento.
- Presets de audio e layout.
- Salvamento/carregamento de configuracao.
- Interface desktop empacotavel em `.exe`.
- Temas visuais e suporte a idioma PT/EN.
- Assistente de IA integrado por API key.

## Controle de audio

O sistema permite controlar os principais blocos de processamento do ADAU1452 diretamente pela interface:

- Volume master.
- Ganho de entrada.
- Ganho de saida.
- Mute por canal.
- Inversao de fase.
- Matriz de roteamento.
- Ganhos individuais dos crosspoints da matriz.
- EQ de entrada.
- EQ de saida.
- Crossover HP/LP.
- Limiter.
- Delay de saida.

Os comandos sao enviados diretamente ao firmware, que atualiza os parametros do ADAU1452 usando os enderecos exportados pelo SigmaStudio.

## Matriz 6x8

A matriz permite rotear ate **6 entradas** para **8 saidas**, com controle individual de:

- Ativo/inativo por ponto de matriz.
- Ganho por crosspoint.
- Visualizacao clara de entradas e saidas.
- Sincronizacao com o firmware.

Esse recurso permite configuracoes flexiveis de roteamento para sistemas estereo, multivias, subwoofers, zonas independentes ou setups personalizados.

## Equalizadores

### Entradas

Cada entrada suportada possui EQ de ate **31 bandas**, com controle de:

- Frequencia.
- Ganho.
- Q.
- Tipo de filtro.
- Bypass.
- Presets tonais.

### Saidas

As saidas suportadas possuem EQ dedicado de **7 bandas**, permitindo ajustes finos por via ou por zona.

## Crossover

Os canais de saida suportados possuem crossover com controles de:

- High-pass.
- Low-pass.
- Frequencia.
- Tipo de filtro.
- Inclinacao.
- Bypass/ativacao.

Esse recurso permite uso em sistemas multivias, separacao de subwoofer, alinhamento de faixas e protecao de alto-falantes.

## Limiter

O sistema possui controle de limiter nos canais de saida suportados, com ajuste de:

- Threshold.
- RMS TC.
- Decay/Release.

Alem do controle, o firmware le os readbacks de atuacao do limiter exportados pelo SigmaStudio. A interface mostra a indicacao visual quando o limiter esta atuando.

A leitura do limiter utiliza o mesmo fluxo dos VUs, sem polling separado.

## Delay de saida

Os canais de saida suportados possuem delay ajustavel, util para alinhamento temporal entre:

- Subwoofer e vias principais.
- Drivers em sistemas multivias.
- Caixas fisicamente desalinhadas.
- Pontos de escuta diferentes.

O delay e aplicado no ADAU1452 em amostras, convertido a partir do valor em milissegundos na interface.

## VUs e calibracao

O sistema possui VUs digitais em LED e VUs analogicos.

A leitura dos VUs vem dos blocos RTA/RMS do SigmaStudio, enviada pelo firmware ao frontend com valor percentual e tambem em **dB x10**, permitindo maior precisao visual.

A calibracao segue a relacao:

```text
VU = RTA_dB + 18
```

Referencia usada:

```text
RTA -38 dB -> -20 VU
RTA -28 dB -> -10 VU
RTA -21 dB ->  -3 VU
RTA -18 dB ->   0 VU
RTA -15 dB ->  +3 VU
```

Os VUs analogicos usam imagem dedicada de alta qualidade e interpolacao para melhor leitura visual.

## Supervisor visual

O modo Supervisor permite criar uma tela operacional personalizada com:

- Widgets de VU.
- Knobs.
- Speakers.
- Schematic blocks.
- Audio player.
- Bargraph.
- Display de 7 segmentos.
- Pontos de conexao.
- Links visuais.
- Snap/grid.
- Edicao de layout.
- Exportacao/importacao de layout.

Esse modo permite montar uma visao grafica do sistema de audio, util para operacao, demonstracao e monitoramento.

## Presets e persistencia

O sistema possui suporte a:

- Salvamento local de presets.
- Carregamento automatico de layout.
- Exportacao/importacao de layout `.json`.
- Salvamento de parametros no dispositivo.
- Aplicacao automatica de preset ao conectar.

O layout validado pode ser empacotado junto com o aplicativo Electron para iniciar a aplicacao com uma configuracao padrao.

## Comunicacao

O sistema suporta dois modos principais de comunicacao:

- **CYD Wi-Fi / WebSocket**
- **Serial / Web Serial / Electron Serial**

O modo Wi-Fi permite uso sem cabo USB apos o dispositivo estar na rede correta. O modo Serial permite configuracao direta, gravacao e testes locais.

## Aplicativo desktop

O frontend pode ser empacotado como aplicativo Windows usando Electron.

Recursos do aplicativo:

- Janela sem moldura customizada.
- Botoes de minimizar, maximizar/restaurar e fechar.
- Icone proprio do AC680PRO.
- Build release normal, sem limitacao trial.
- Layout padrao incluido no pacote.
- Saida em instalador `.exe`.

Comando de build:

```powershell
cd F:\Projetos\ESP32-CYD-ADAU1452\dsp-controller
npm run electron:build
```

## Interface

A interface foi construida para uso tecnico e operacional, com foco em:

- Densidade de informacao.
- Controles diretos.
- Leitura rapida.
- Temas visuais.
- Idiomas PT/EN.
- Operacao em desktop.
- Compatibilidade com uso em campo.

## Assistente de IA

O sistema possui area para configuracao de API key e uso de assistente de IA integrado. Esse recurso pode ser usado para apoio, diagnostico, explicacoes e auxilio operacional, dependendo do provedor configurado.

## Estado atual

Ate este ponto, o sistema ja integra:

- Firmware ESP32-CYD.
- DSP ADAU1452.
- Export SigmaStudio atualizado.
- Frontend React.
- Aplicativo Electron.
- Comunicacao Wi-Fi/Serial.
- Matriz, EQs, crossover, limiter, delay e VUs.
- Readback de limiter.
- Calibracao documentada de VUs.
- Release desktop normal.

A proxima evolucao planejada e a funcao experimental de **canais vinculados**, onde comandos aplicados a um canal poderao ser replicados automaticamente para outros canais selecionados, inicialmente apenas no frontend.
