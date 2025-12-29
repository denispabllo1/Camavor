import React, { useState } from 'react';
import { Heart, Sparkles, Scroll } from 'lucide-react';

export default function D20KissSimulator() {
  const [rolling, setRolling] = useState(false);
  const [result, setResult] = useState(null);
  const [rotation, setRotation] = useState(0);

  const narratives = {
    1: {
      title: "💀 FALHA CRÍTICA DEVASTADORA",
      story: "Porra! Tu se inclina pro beijo e tropeça nos próprios pés feito um idiota! Cai de cara no chão levantando poeira. Denis continua desmaiado e tu ganha -5 em Carisma. O título 'Aventureiro Inútil' foi desbloqueado. Que merda, hein? Melhor treinar coordenação motora antes da próxima, seu mané.",
      color: "from-red-900 to-red-700",
      glow: "shadow-red-500/50"
    },
    2: {
      title: "😅 Friendzone do Caralho",
      story: "Tu junta coragem e se aproxima do Denis desmaiado... mas tua mão escorrega e acaba dando um tapinha amigável na barriga dele. Denis acorda confuso e diz 'valeu, parceiro'. Que bosta. O debuff 'Amigo da Madrugada' foi aplicado permanentemente. Tenta de novo daqui uns 3 anos.",
      color: "from-orange-800 to-orange-600",
      glow: "shadow-orange-500/50"
    },
    3: {
      title: "🤝 Abraço Patético",
      story: "Tua intenção era nobre, mas que execução de merda! Tu se aproxima pro beijo mas no último segundo fica com cagaço e só abraça o mago gordinho. Denis continua dormindo. É aconchegante? Talvez. É o que tu queria? Com certeza não. +2 em Amizade Inútil, -3 em Dignidade.",
      color: "from-orange-700 to-yellow-700",
      glow: "shadow-orange-400/50"
    },
    4: {
      title: "😬 Quase Lá, Mas Se Fodeu",
      story: "Caralho, tava quase! Tu se aproxima do Denis, o momento tá perfeito, até uma brisa mágica passa... quando do nada um goblin aparece gritando sobre impostos atrasados. O momento foi pro caralho. Denis continua apagado. Teste de Sorte: FALHOU. Tenta outra hora, azarado.",
      color: "from-yellow-800 to-yellow-600",
      glow: "shadow-yellow-500/50"
    },
    5: {
      title: "😊 Beijinho Meia-Boca",
      story: "Tu tenta ser ousado mas na hora H o cu tranca. Desvia pro ombro gorducho do Denis e deixa um beijinho ali. Ele se mexe mas não acorda. É fofo? Talvez. Resolve alguma coisa? Porra nenhuma. +1 em Fofura Inútil, -1 em Testosterona. Cresce esses colhões, guerreiro!",
      color: "from-yellow-700 to-amber-600",
      glow: "shadow-yellow-400/50"
    },
    6: {
      title: "💭 Beijo na Imaginação",
      story: "Puta que pariu! Tu fecha os olhos e imagina o beijo salvador... mas só isso mesmo. Na vida real não rolou merda nenhuma. Denis continua roncando. Tuas habilidades de sonhar acordado tão em dia, mas tua habilidade de fazer acontecer tá uma bosta. Sai da Matrix, mano!",
      color: "from-amber-700 to-amber-500",
      glow: "shadow-amber-400/50"
    },
    7: {
      title: "😚 Beijo Torto na Bochecha",
      story: "Caralho! Tu mira na boca mas acerta a bochecha gorda do Denis! O mago acorda meio confuso, coça a barriga e diz 'que porra foi essa?'. Não era o plano, mas funcionou! Tipo. Ele tá vivo pelo menos. +10 XP em Romance Capenga. Achievement 'Quase Lá' desbloqueado.",
      color: "from-amber-600 to-yellow-500",
      glow: "shadow-amber-300/50"
    },
    8: {
      title: "🔥 Esquentou a Parada",
      story: "Porra, a tensão tá alta! Tu se aproxima do Denis, as mãos tremem, o coração acelera... tu quase encosta os lábios quando um bando de aventureiros bêbados passa cantando. Boss de Interrupção Filha da Puta apareceu! Mas a vibe tá boa. Denis até mexeu o braço. +3 em Tesão, -5 em Timing.",
      color: "from-yellow-600 to-orange-500",
      glow: "shadow-yellow-300/50"
    },
    9: {
      title: "💋 Beijo Rápido que Salvou!",
      story: "Caralho, conseguiu! Tu planta um beijo rápido mas eficaz! Denis abre os olhos assustado, se levanta cambaleando e grita 'QUEM TA AÍ?!'. Missão cumprida! O veneno foi neutralizado. Achievement 'Quebrou a Maldição' desbloqueado! +15 XP. Agora corre antes que ele faça perguntas!",
      color: "from-green-700 to-green-500",
      glow: "shadow-green-400/50"
    },
    10: {
      title: "😘 Beijo Decente que Funcionou",
      story: "Porra, não foi perfeito mas foi! Um beijo apropriado, no timing certo. Denis acorda, pisca os olhos e diz 'caralho, que veneno forte'. Ele tá salvo! Sem fogos de artifício, mas deu certo. +5 em Eficiência, +3 em Confiança. Quest Progrediu, seu foda!",
      color: "from-green-600 to-emerald-500",
      glow: "shadow-green-300/50"
    },
    11: {
      title: "💖 Beijo com Efeito Duplo",
      story: "Caralho! O primeiro beijo foi tão bom que Denis acordou E puxou tu de volta pro segundo! Teste de Reflexo: SUCESSO CRÍTICO! Os lábios dançam perfeitamente. Uma fênix canta aprovando. Buff 'Beijo Duplo' aplicado! +7 em Autoestima, +5 em Lendas Locais.",
      color: "from-emerald-600 to-teal-500",
      glow: "shadow-emerald-300/50"
    },
    12: {
      title: "🌹 Beijo Digno de Novela",
      story: "PUTA MERDA! Vocês se beijam e o mundo para! As pessoas passam mas vocês tão noutro plano. Uma trilha sonora épica rola na tua cabeça. Denis acorda emocionado. É o tipo de beijo que merece câmera lenta. Seu personagem evoluiu! Título 'Romântico Fodão' desbloqueado!",
      color: "from-teal-600 to-cyan-500",
      glow: "shadow-teal-300/50"
    },
    13: {
      title: "🎬 Beijo Cinematográfico",
      story: "CARALHO! Vocês se beijam e começa a chover! Um raio ilumina vocês. Denis acorda e passa a mão na tua cara. Tu puxa ele mais perto. Se isso fosse filme, ganhava Oscar. Achievement Raro 'Beijo Hollywoodiano' desbloqueado! +10 em Carisma, +5 em Fama!",
      color: "from-cyan-600 to-blue-500",
      glow: "shadow-cyan-300/50"
    },
    14: {
      title: "⏰ Beijo que Parou o Caralho do Tempo",
      story: "QUE PORRA É ESSA?! Quando teus lábios tocam os do Denis, o tempo literalmente CONGELA! Vocês ficam ali suspensos num momento eterno e mágico. Quando se separam, Denis tá brilhando. Passou segundos mas pareceu uma vida. Magia de nível 9 detectada! Que bruxaria é essa?!",
      color: "from-blue-600 to-indigo-500",
      glow: "shadow-blue-300/50"
    },
    15: {
      title: "💨 Beijo Sufocante Fodástico",
      story: "PUTA QUE PARIU! Esse beijo é TÃO intenso que vocês LITERALMENTE esquecem de respirar! Quando se separam, ambos ofegantes, suando, Denis grita 'CARALHO, QUE BEIJO FOI ESSE?!'. Status aplicado: 'Hipnotizado Total'. Duração: Permanente. Fudeu, era pra ser só um beijo!",
      color: "from-indigo-600 to-purple-500",
      glow: "shadow-indigo-300/50"
    },
    16: {
      title: "🦋 Tsunami de Borboletas na Barriga",
      story: "CARALHO! Esse beijo liberou uma REVOADA ABSURDA de borboletas no estômago! Denis acorda sorrindo feito bobo, tu também tá voando. Vocês tão literalmente 10cm acima do chão. Efeito 'Levitação Romântica' ativado por 24h! Os outros aventureiros tão com inveja pra caralho!",
      color: "from-purple-600 to-fuchsia-500",
      glow: "shadow-purple-300/50"
    },
    17: {
      title: "⭐ Beijo de Proporções Épicas",
      story: "BEIJO ÉPICO CARREGANDO... 100%! PORRA! Esse beijo vai entrar pros anais da história de Dungeons & Dragons! Bardos vão cantar sobre isso! Um cometa passa testemunhando! Denis acorda glorioso! Classe prestige 'Mestre do Beijo' desbloqueada! Todos os NPCs tão é fodidos de inveja!",
      color: "from-fuchsia-600 to-pink-500",
      glow: "shadow-fuchsia-300/50"
    },
    18: {
      title: "🏆 Beijo Lendário Conquistado",
      story: "ITEM LENDÁRIO DROPADO, PORRA! Esse beijo é TÃO perfeito que tu ouve música celestial! Anjos choram! Cupido anota no caderninho dele! Denis acorda transformado, brilhando! É apaixonado, delicado e INTENSO ao mesmo tempo! Achievement 'Beijo Lendário' (0.01% dos jogadores)! Tu é o FODA, campeão!",
      color: "from-pink-600 to-rose-500",
      glow: "shadow-pink-300/50"
    },
    19: {
      title: "👑 Beijo Real de Conto de Fadas",
      story: "PORRA! Tu é príncipe agora! Esse beijo tem magia VERDADEIRA! Flores brotam ao redor! Passarinhos cantam! Uma luz dourada e cintilante envolve vocês! Denis acorda com uma porra de uma auréola! O universo grita: 'ALMAS GÊMEAS CONFIRMADAS'! Status: Blessed by the Fucking Gods! Forever buff aplicado!",
      color: "from-rose-600 to-pink-500",
      glow: "shadow-rose-300/50"
    },
    20: {
      title: "💖✨ CRÍTICO ABSOLUTO - BEIJO DIVINO DO CARALHO",
      story: "🎆 EXPLOSÃO DE DADOS CRÍTICOS! 🎆 CARALHO! O IMPOSSÍVEL ACONTECEU! NÃO É BEIJO, É FUSÃO TOTAL DE ALMAS! O PRÓPRIO DESTINO CONSPIROU PRA ISSO! Fogos explodem, violinos tocam, o céu se ABRE e uma luz DIVINA banha vocês! Denis acorda TRANSCENDIDO! Vocês passaram pro plano astral! As leis da física se FODERAM! CONQUISTA MÍTICA: 'TRUE LOVE'S KISS'! TODAS stats MAXIMIZADAS! +∞ em TUDO! PARABÉNS, GRANDE MESTRE SUPREMO DO ROMANCE! TU É O REI DA PORRA TODA! 👑💕✨",
      color: "from-pink-500 via-purple-500 to-rose-500",
      glow: "shadow-pink-500/80 shadow-2xl"
    }
  };

  const rollDice = () => {
    setRolling(true);
    setResult(null);
    
    let spins = 0;
    const maxSpins = 40;
    
    const spinInterval = setInterval(() => {
      setRotation(prev => prev + 18);
      spins++;
      
      if (spins >= maxSpins) {
        clearInterval(spinInterval);
        const finalResult = Math.floor(Math.random() * 20) + 1;
        
        setTimeout(() => {
          setResult(finalResult);
          setRolling(false);
        }, 500);
      }
    }, 30);
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900 flex items-center justify-center p-4">
      <style>{`
        .perspective-1000 {
          perspective: 1000px;
        }
        .preserve-3d {
          transform-style: preserve-3d;
        }
      `}</style>
      <div className="max-w-2xl w-full">
        {/* Header */}
        <div className="text-center mb-8 space-y-4">
          <div className="flex justify-center gap-3 mb-4">
            <Scroll className="text-purple-300" size={40} />
            <Heart className="text-pink-400 animate-pulse" size={40} fill="currentColor" />
            <Sparkles className="text-purple-300" size={40} />
          </div>
          <h1 className="text-5xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-pink-400 via-purple-400 to-pink-400">
            Quest do Beijo Mágico
          </h1>
          <div className="bg-black/40 backdrop-blur-sm rounded-2xl p-6 border border-purple-500/30 max-w-xl mx-auto">
            <p className="text-purple-100 text-lg leading-relaxed">
              🧙‍♂️ <span className="font-bold text-pink-300">Olá, aventureiro!</span> Você chegou nesta jornada e encontra o <span className="font-bold text-yellow-300">Mago Gordinho Denis</span> caído no chão, desmaiado! 
            </p>
            <p className="text-purple-100 text-lg leading-relaxed mt-3">
              💀 Ele foi picado por um <span className="font-bold text-red-400">Wyvern venenoso</span> e só vai acordar com um beijo verdadeiro!
            </p>
            <p className="text-pink-300 text-xl font-bold mt-4">
              ⚔️ Gire o Dado de Ação e descubra seu destino! ⚔️
            </p>
          </div>
        </div>

        {/* Dice Container */}
        <div className="bg-black/30 backdrop-blur-sm rounded-3xl shadow-2xl p-8 mb-6 border border-purple-500/30">
          <div className="flex justify-center py-12 perspective-1000">
            <div 
              className="relative preserve-3d"
              style={{ 
                width: '180px',
                height: '180px',
                transform: rolling 
                  ? `rotateX(${rotation * 3}deg) rotateY(${rotation * 4}deg) rotateZ(${rotation * 2}deg)`
                  : result 
                    ? `rotateX(${result * 15}deg) rotateY(${result * 20}deg)`
                    : 'rotateX(20deg) rotateY(20deg)',
                transition: rolling ? 'none' : 'transform 1s cubic-bezier(0.34, 1.56, 0.64, 1)',
                transformStyle: 'preserve-3d'
              }}
            >
              {/* D20 Icosahedron Faces */}
              {[...Array(20)].map((_, i) => {
                const rotations = [
                  'rotateY(0deg) translateZ(90px)',
                  'rotateY(36deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(72deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(108deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(144deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(180deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(216deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(252deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(288deg) rotateX(20deg) translateZ(90px)',
                  'rotateY(324deg) rotateX(20deg) translateZ(90px)',
                  'rotateX(60deg) translateZ(90px)',
                  'rotateX(60deg) rotateY(72deg) translateZ(90px)',
                  'rotateX(60deg) rotateY(144deg) translateZ(90px)',
                  'rotateX(60deg) rotateY(216deg) translateZ(90px)',
                  'rotateX(60deg) rotateY(288deg) translateZ(90px)',
                  'rotateX(-60deg) translateZ(90px)',
                  'rotateX(-60deg) rotateY(72deg) translateZ(90px)',
                  'rotateX(-60deg) rotateY(144deg) translateZ(90px)',
                  'rotateX(-60deg) rotateY(216deg) translateZ(90px)',
                  'rotateX(-60deg) rotateY(288deg) translateZ(90px)'
                ];
                
                return (
                  <div
                    key={i}
                    className="absolute w-full h-full"
                    style={{
                      transform: rotations[i],
                      transformStyle: 'preserve-3d'
                    }}
                  >
                    <div className="w-full h-full flex items-center justify-center">
                      <div className="w-24 h-24 bg-gradient-to-br from-purple-500/60 to-pink-500/60 backdrop-blur-md border-2 border-purple-300/40 shadow-lg flex items-center justify-center"
                        style={{
                          clipPath: 'polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%)',
                          boxShadow: 'inset 0 0 20px rgba(255, 255, 255, 0.1), 0 0 30px rgba(168, 85, 247, 0.4)'
                        }}
                      >
                        <span className="text-white text-3xl font-bold drop-shadow-lg">
                          {i + 1}
                        </span>
                      </div>
                    </div>
                  </div>
                );
              })}
              
              {/* Glow effect */}
              <div className="absolute inset-0 rounded-full bg-purple-500/20 blur-3xl animate-pulse pointer-events-none" 
                style={{ transform: 'translateZ(-50px)' }}
              ></div>
            </div>
          </div>

          <button
            onClick={rollDice}
            disabled={rolling}
            className="w-full bg-gradient-to-r from-purple-600 via-pink-600 to-purple-600 text-white font-bold py-5 rounded-2xl shadow-lg shadow-purple-500/50 hover:shadow-xl hover:shadow-pink-500/50 transform hover:scale-105 transition-all disabled:opacity-50 disabled:cursor-not-allowed disabled:transform-none text-xl border border-purple-400/50"
          >
            {rolling ? '🎲 Os dados rolam...' : '🎲 Rolar o Dado do Destino!'}
          </button>
        </div>

        {/* Narrative Result */}
        {result && (
          <div className={`bg-gradient-to-br ${narratives[result].color} rounded-3xl p-8 border-2 border-white/20 ${narratives[result].glow} animate-in fade-in slide-in-from-bottom-4 duration-700`}>
            <div className="text-center mb-4">
              <div className="inline-block bg-black/30 px-6 py-2 rounded-full mb-4">
                <span className="text-white text-3xl font-bold">🎲 {result}</span>
              </div>
              <h2 className="text-2xl md:text-3xl font-bold text-white mb-4">
                {narratives[result].title}
              </h2>
            </div>
            <div className="bg-black/20 backdrop-blur-sm rounded-2xl p-6 border border-white/10">
              <p className="text-white text-lg leading-relaxed text-center md:text-left">
                {narratives[result].story}
              </p>
            </div>
          </div>
        )}

        {/* Footer */}
        <div className="text-center mt-6 text-purple-300 text-sm">
          <p>⚔️ Sistema de RPG: 1 = Falha Crítica | 20 = Crítico Perfeito ⚔️</p>
        </div>
      </div>
    </div>
  );
}
