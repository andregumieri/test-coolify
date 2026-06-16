<template>
  <div class="body-wrapper">

    <!-- MARQUEE TOPO -->
    <div class="marquee-bar">
      <marquee behavior="scroll" direction="left" scrollamount="4">
        🍺 BEM-VINDO AO CERVEJAMANIA.COM.BR 🍺 &nbsp;&nbsp;&nbsp; O MELHOR SITE DE CERVEJAS DO BRASIL DESDE 2001! &nbsp;&nbsp;&nbsp; 🍻 MAIS DE 5.000 VISITANTES! 🍻 &nbsp;&nbsp;&nbsp; ADICIONE AOS FAVORITOS! &nbsp;&nbsp;&nbsp; 🍺 BEM-VINDO AO CERVEJAMANIA.COM.BR 🍺
      </marquee>
    </div>

    <!-- HEADER -->
    <table class="header-table" width="100%" cellpadding="0" cellspacing="0">
      <tr>
        <td class="header-left">
          <span class="logo-emoji">🍺</span>
          <div class="site-title">
            <span class="title-beer">Cerveja</span><span class="title-mania">Mania</span><span class="title-com">.com.br</span>
          </div>
          <div class="site-slogan">&gt;&gt; Porque a vida é melhor com uma gelada!! &lt;&lt;</div>
        </td>
        <td class="header-right">
          <div class="visitor-counter">
            <div class="counter-label">VISITANTES:</div>
            <div class="counter-digits">
              <span v-for="d in counterDigits" :key="d.id" class="digit">{{ d.val }}</span>
            </div>
          </div>
          <div class="online-now">👁️ {{ onlineNow }} pessoas online agora!</div>
          <div class="last-update">Última atualização: 14/03/2003</div>
        </td>
      </tr>
    </table>

    <!-- NAVEGAÇÃO -->
    <table class="nav-table" width="100%" cellpadding="2" cellspacing="2">
      <tr>
        <td v-for="item in navItems" :key="item.id" class="nav-item" @click="activeSection = item.id">
          <a href="#" @click.prevent="activeSection = item.id" :class="{ 'nav-link': true, 'nav-active': activeSection === item.id }">
            {{ item.label }}
          </a>
        </td>
      </tr>
    </table>

    <!-- CONTENT AREA -->
    <table class="content-table" width="100%" cellpadding="0" cellspacing="0">
      <tr>

        <!-- SIDEBAR ESQUERDA -->
        <td class="sidebar-left" valign="top" width="160">
          <div class="sidebar-box">
            <div class="sidebar-title">🔥 MAIS VISTOS</div>
            <ul class="sidebar-list">
              <li v-for="item in topBeers" :key="item">
                <a href="#" @click.prevent class="sidebar-link">{{ item }}</a>
              </li>
            </ul>
          </div>
          <div class="sidebar-box">
            <div class="sidebar-title">📊 ENQUETE</div>
            <div class="poll-question">Qual a melhor cerveja?</div>
            <div v-for="opt in pollOptions" :key="opt.label" class="poll-option">
              <input type="radio" name="poll" :value="opt.label" v-model="pollVote" />
              {{ opt.label }}<br />
              <div class="poll-bar-bg">
                <div class="poll-bar" :style="{ width: opt.pct + '%' }"></div>
              </div>
              <span class="poll-pct">{{ opt.pct }}%</span>
            </div>
            <button class="vote-btn" @click="votou = true">VOTAR!</button>
            <div v-if="votou" class="vote-thanks">Obrigado pelo voto!! :D</div>
          </div>
          <div class="sidebar-box">
            <div class="sidebar-title">🔗 LINKS</div>
            <ul class="sidebar-list">
              <li><a href="#" @click.prevent class="sidebar-link">Cerveja.net</a></li>
              <li><a href="#" @click.prevent class="sidebar-link">BebidaOnline</a></li>
              <li><a href="#" @click.prevent class="sidebar-link">PubBrasil</a></li>
              <li><a href="#" @click.prevent class="sidebar-link">ChopeAqui</a></li>
              <li><a href="#" @click.prevent class="sidebar-link">Bolinha's Bar</a></li>
            </ul>
          </div>
          <div class="sidebar-box banners">
            <div class="sidebar-title">📢 BANNERS</div>
            <div class="banner-item">88x31 FREE!</div>
            <div class="banner-item2">Coloque o nosso banner!</div>
          </div>
        </td>

        <!-- CONTEÚDO PRINCIPAL -->
        <td class="main-content" valign="top">

          <!-- HOME -->
          <div v-if="activeSection === 'home'">
            <div class="section-title">
              <span class="new-badge">NEW!</span>
              🍺 BEM-VINDO AO CERVEJAMANIA!
            </div>
            <div class="welcome-box">
              <p>
                Olá cervejeiro(a)!! Seja muito bem-vindo ao <strong>CervejaMania.com.br</strong>, o MELHOR e MAIOR site
                sobre cervejas do Brasil inteiro!! Aqui você vai encontrar <u>TUDO</u> sobre a bebida mais gostosa do mundo!!
              </p>
              <p>
                Este site foi criado em <strong>Janeiro de 2001</strong> pelo <em>Zé da Cerveja</em> (ze_da_cerveja@hotmail.com)
                com muito carinho pra todos os amantes da boa e velha <strong>GELADA</strong>!! 🍺🍺🍺
              </p>
              <p style="color:#ff0000; font-weight:bold;">
                *** ATENÇÃO: Este site é melhor visualizado no Internet Explorer 6.0 com resolução 800x600 ***
              </p>
            </div>

            <div class="section-title">📰 ÚLTIMAS NOTÍCIAS</div>
            <div v-for="news in newsItems" :key="news.id" class="news-item">
              <div class="news-date">{{ news.date }}</div>
              <div class="news-title">{{ news.title }}</div>
              <div class="news-body">{{ news.body }}</div>
              <hr class="hr-dotted" />
            </div>

            <div class="section-title">⭐ CERVEJA DA SEMANA</div>
            <table class="beer-of-week" cellpadding="8">
              <tr>
                <td class="beer-emoji-cell">🍺</td>
                <td>
                  <strong class="beer-name-big">Brahma Duplo Malte</strong><br />
                  <span class="beer-type">Tipo: Lager • Teor: 6,5% • País: Brasil</span><br /><br />
                  <em>"A Brahma Duplo Malte chegou pra sacudir os botecos de todo o Brasil!
                  Com seu sabor mais encorpado e aquela cor dourada inconfundível, ela é a pedida certa
                  pra quem quer uma cerveja diferente sem precisar gastar muito. Muito boa!!"</em><br /><br />
                  <span class="rating">Nota do Zé: ⭐⭐⭐⭐ (4/5)</span>
                </td>
              </tr>
            </table>
          </div>

          <!-- CERVEJAS -->
          <div v-if="activeSection === 'cervejas'">
            <div class="section-title">📋 GUIA DE CERVEJAS</div>
            <p class="intro-text">Aqui estão todas as cervejas que já provamos e avaliamos!! Clique no nome pra ver mais detalhes!</p>
            <table class="beers-table" width="100%" cellpadding="4" cellspacing="1">
              <tr class="beers-header">
                <th>Nome</th>
                <th>Tipo</th>
                <th>País</th>
                <th>Teor Alc.</th>
                <th>Nota</th>
              </tr>
              <tr v-for="(beer, i) in beers" :key="beer.name" :class="i % 2 === 0 ? 'row-even' : 'row-odd'">
                <td><a href="#" @click.prevent="selectedBeer = beer" class="beer-link">{{ beer.name }}</a></td>
                <td>{{ beer.type }}</td>
                <td>{{ beer.country }}</td>
                <td>{{ beer.abv }}%</td>
                <td>{{ beer.stars }}</td>
              </tr>
            </table>

            <div v-if="selectedBeer" class="beer-detail-box">
              <div class="beer-detail-title">🍺 {{ selectedBeer.name }}</div>
              <p><strong>Tipo:</strong> {{ selectedBeer.type }}</p>
              <p><strong>País:</strong> {{ selectedBeer.country }}</p>
              <p><strong>Teor Alcoólico:</strong> {{ selectedBeer.abv }}%</p>
              <p><strong>Cervejaria:</strong> {{ selectedBeer.brewery }}</p>
              <p><strong>Descrição:</strong> {{ selectedBeer.desc }}</p>
              <p><strong>Nota:</strong> {{ selectedBeer.stars }}</p>
              <button class="close-btn" @click="selectedBeer = null">[Fechar]</button>
            </div>
          </div>

          <!-- RECEITAS -->
          <div v-if="activeSection === 'receitas'">
            <div class="section-title">🍳 RECEITAS COM CERVEJA</div>
            <p class="intro-text">Cerveja não é só pra beber não!! Confira essas receitas INCRÍVEIS que o nosso chef Toninho preparou especialmente pro CervejaMania!!</p>
            <div v-for="recipe in recipes" :key="recipe.name" class="recipe-box">
              <div class="recipe-title">{{ recipe.emoji }} {{ recipe.name }}</div>
              <div class="recipe-meta">Dificuldade: {{ recipe.dificuldade }} | Tempo: {{ recipe.tempo }}</div>
              <strong>Ingredientes:</strong>
              <ul class="recipe-list">
                <li v-for="ing in recipe.ingredientes" :key="ing">{{ ing }}</li>
              </ul>
              <strong>Modo de Preparo:</strong>
              <p class="recipe-prep">{{ recipe.preparo }}</p>
            </div>
          </div>

          <!-- CURIOSIDADES -->
          <div v-if="activeSection === 'curiosidades'">
            <div class="section-title">🤓 VOCÊ SABIA??</div>
            <p class="intro-text">Fatos IMPRESSIONANTES sobre a nossa querida cerveja que você provavelmente não sabia!!</p>
            <div v-for="(fact, i) in facts" :key="i" class="fact-box">
              <span class="fact-num">{{ i + 1 }}.</span> {{ fact }}
            </div>

            <div class="section-title" style="margin-top:16px">🏆 RECORDES DE CERVEJA</div>
            <table class="records-table" cellpadding="4">
              <tr class="beers-header">
                <th>Recorde</th>
                <th>Detentor</th>
                <th>Valor</th>
              </tr>
              <tr v-for="(rec, i) in records" :key="i" :class="i % 2 === 0 ? 'row-even' : 'row-odd'">
                <td>{{ rec.record }}</td>
                <td>{{ rec.holder }}</td>
                <td>{{ rec.value }}</td>
              </tr>
            </table>
          </div>

          <!-- FÓRUM -->
          <div v-if="activeSection === 'forum'">
            <div class="section-title">💬 FÓRUM DO CERVEJAMANIA</div>
            <p class="intro-text">Deixe seu recado! Total de mensagens: <strong>{{ messages.length }}</strong></p>
            <div class="forum-form">
              <table cellpadding="4">
                <tr>
                  <td class="form-label">Seu nick:</td>
                  <td><input v-model="newMsg.nick" type="text" class="form-input" maxlength="20" placeholder="Ex: ZeDaCerveja" /></td>
                </tr>
                <tr>
                  <td class="form-label">Mensagem:</td>
                  <td><textarea v-model="newMsg.text" class="form-textarea" rows="3" cols="40" maxlength="200"></textarea></td>
                </tr>
                <tr>
                  <td></td>
                  <td>
                    <button class="send-btn" @click="sendMessage">ENVIAR MENSAGEM >></button>
                    <button class="clear-btn" @click="newMsg = { nick: '', text: '' }">LIMPAR</button>
                  </td>
                </tr>
              </table>
            </div>
            <div v-for="msg in messages" :key="msg.id" class="message-box">
              <div class="msg-header">
                <span class="msg-nick">{{ msg.nick }}</span>
                <span class="msg-date"> disse em {{ msg.date }}:</span>
              </div>
              <div class="msg-text">{{ msg.text }}</div>
            </div>
          </div>

          <!-- CONTATO -->
          <div v-if="activeSection === 'contato'">
            <div class="section-title">📧 FALE CONOSCO</div>
            <div class="contact-box">
              <p>Quer entrar em contato com a equipe do CervejaMania? Manda um e-mail pra gente!!</p>
              <table cellpadding="6">
                <tr>
                  <td class="contact-label">Webmaster:</td>
                  <td><a href="mailto:ze_da_cerveja@hotmail.com" class="email-link">ze_da_cerveja@hotmail.com</a></td>
                </tr>
                <tr>
                  <td class="contact-label">Chef Receitas:</td>
                  <td><a href="mailto:toninho_chef@bol.com.br" class="email-link">toninho_chef@bol.com.br</a></td>
                </tr>
                <tr>
                  <td class="contact-label">ICQ:</td>
                  <td><span class="icq">12345678</span> (Zé da Cerveja)</td>
                </tr>
                <tr>
                  <td class="contact-label">MSN:</td>
                  <td>ze_da_cerveja@hotmail.com</td>
                </tr>
              </table>
              <hr class="hr-dotted" />
              <p class="contact-note">
                📌 <strong>ATENÇÃO:</strong> Este site é feito nas horas vagas e com muito amor!! Se você curtiu, manda um
                e-mail falando o que achou! Se não curtiu, manda também hehehe!! 😄
              </p>
              <p>
                Para <strong>parcerias</strong> e <strong>troca de banners</strong>, envie e-mail com o assunto
                <em>"PARCERIA CERVEJAMANIA"</em>. Tamanho aceito: 88x31, 468x60.
              </p>
            </div>

            <div class="section-title">🗺️ ONDE FICA O ZÉ?</div>
            <div class="map-fake">
              [ Mapa não disponível - Você precisa do Macromedia Flash 5 para visualizar ]<br />
              <a href="#" @click.prevent class="sidebar-link">Clique aqui pra baixar o Flash</a>
            </div>
          </div>

        </td>

        <!-- SIDEBAR DIREITA -->
        <td class="sidebar-right" valign="top" width="150">
          <div class="sidebar-box">
            <div class="sidebar-title">🌡️ TEMPERATURA</div>
            <div class="temp-display">{{ temp }}°C</div>
            <div class="temp-label">São Paulo agora</div>
            <div class="temp-beer">{{ tempAdvice }}</div>
          </div>
          <div class="sidebar-box">
            <div class="sidebar-title">📅 DATA</div>
            <div class="date-display">{{ currentDate }}</div>
            <div class="time-display">{{ currentTime }}</div>
          </div>
          <div class="sidebar-box">
            <div class="sidebar-title">😂 PIADA</div>
            <div class="joke-text">{{ currentJoke }}</div>
            <button class="joke-btn" @click="nextJoke">Próxima &gt;&gt;</button>
          </div>
          <div class="sidebar-box">
            <div class="sidebar-title">🎵 AGORA TOCANDO</div>
            <div class="music-player">
              <div class="music-title">♪ {{ currentSong.name }}</div>
              <div class="music-artist">{{ currentSong.artist }}</div>
              <div class="music-controls">
                [▶ PLAY] [⏸ PAUSE]<br/>
                <em style="font-size:9px">(requer Windows Media Player)</em>
              </div>
            </div>
          </div>
          <div class="sidebar-box">
            <div class="sidebar-title">🔔 NOVIDADES</div>
            <div class="news-ticker">
              <div v-for="tick in tickers" :key="tick" class="ticker-item">• {{ tick }}</div>
            </div>
          </div>
        </td>
      </tr>
    </table>

    <!-- FOOTER -->
    <div class="footer">
      <div class="footer-text">
        © 2001-2003 CervejaMania.com.br - Todos os direitos reservados<br />
        Desenvolvido por <strong>Zé da Cerveja</strong> usando <em>Notepad</em> e muito amor!! 🍺<br />
        <span class="footer-small">
          Melhor visualizado em IE 6.0 | Resolução 800x600 | Requer Flash 5 e Windows Media Player
        </span>
      </div>
      <div class="footer-icons">
        <span class="badge">IE 6</span>
        <span class="badge">800x600</span>
        <span class="badge">Flash 5</span>
        <span class="badge">HTML 4.01</span>
      </div>
      <div class="footer-hits">
        Você é o visitante número <strong>{{ hitCounter }}</strong> desde 15/01/2001
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

// NAV
const navItems = [
  { id: 'home', label: '🏠 INÍCIO' },
  { id: 'cervejas', label: '🍺 CERVEJAS' },
  { id: 'receitas', label: '🍳 RECEITAS' },
  { id: 'curiosidades', label: '🤓 CURIOSIDADES' },
  { id: 'forum', label: '💬 FÓRUM' },
  { id: 'contato', label: '📧 CONTATO' },
]
const activeSection = ref('home')

// CONTADOR
const counterDigits = ref([
  { id: 0, val: '0' }, { id: 1, val: '5' }, { id: 2, val: '2' },
  { id: 3, val: '3' }, { id: 4, val: '4' }, { id: 5, val: '7' },
])
const onlineNow = ref(23)
const hitCounter = ref('052.347')

// SIDEBAR TOP
const topBeers = ['Skol Puro Malte', 'Brahma Extra', 'Antarctica', 'Itaipava', 'Devassa']

// POLL
const pollOptions = ref([
  { label: 'Skol', pct: 38 },
  { label: 'Brahma', pct: 29 },
  { label: 'Antarctica', pct: 18 },
  { label: 'Outra', pct: 15 },
])
const pollVote = ref('')
const votou = ref(false)

// NEWS
const newsItems = [
  {
    id: 1,
    date: '14/03/2003',
    title: '🆕 Nova seção de receitas adicionada!!',
    body: 'Pessoal, finalmente terminei a seção de receitas!! O Chef Toninho mandou 5 receitas incríveis com cerveja. Confiram!!'
  },
  {
    id: 2,
    date: '02/03/2003',
    title: '📊 CervejaMania atinge 50.000 visitantes!!',
    body: 'Incrível!! Em menos de 2 anos chegamos a 50 mil visitantes!! Muito obrigado a todos que acompanham o site. Sem vocês nada disso seria possível!!'
  },
  {
    id: 3,
    date: '14/02/2003',
    title: '❤️ Feliz Dia dos Namorados pra todos!!',
    body: 'E pra celebrar, nada melhor que uma cervejinha gelada com a pessoa amada né!! Saúde a todos!! 🍺🍺'
  },
]

// CERVEJAS
const beers = [
  { name: 'Skol Puro Malte', type: 'Lager', country: '🇧🇷 Brasil', abv: 5.0, stars: '⭐⭐⭐⭐', brewery: 'AmBev', desc: 'A versão premium da Skol com malte 100% puro. Levinha e muito refrescante. Ótima pedida pro calor!' },
  { name: 'Brahma Extra', type: 'Lager', country: '🇧🇷 Brasil', abv: 5.4, stars: '⭐⭐⭐⭐', brewery: 'AmBev', desc: 'Encorpada e saborosa. A Extra tem um amargor mais pronunciado que as outras cervejas mainstream.' },
  { name: 'Antarctica Original', type: 'Pilsen', country: '🇧🇷 Brasil', abv: 4.9, stars: '⭐⭐⭐', brewery: 'AmBev', desc: 'Clássica das clássicas. Levinha e refrescante. A pedida certa pra um churrasquinho!' },
  { name: 'Devassa Tropical', type: 'Lager', country: '🇧🇷 Brasil', abv: 4.7, stars: '⭐⭐⭐⭐', brewery: 'Devassa', desc: 'Com toque tropical, essa cerveja surpreende! Muito boa pra quem quer experimentar algo diferente.' },
  { name: 'Kaiser Gold', type: 'Pilsen', country: '🇧🇷 Brasil', abv: 4.5, stars: '⭐⭐⭐', brewery: 'Kaiser', desc: 'Suave e equilibrada. A Kaiser Gold é uma opção mais acessível pra quem tá no orçamento.' },
  { name: 'Guinness Draught', type: 'Stout', country: '🇮🇪 Irlanda', abv: 4.2, stars: '⭐⭐⭐⭐⭐', brewery: 'Guinness', desc: 'A lendária cerveja preta irlandesa!! Cremosa, com sabor de café e chocolate. Uma experiência única!!' },
  { name: 'Stella Artois', type: 'Pilsen', country: '🇧🇪 Bélgica', abv: 5.0, stars: '⭐⭐⭐⭐', brewery: 'InBev', desc: 'A "cerveja de cinema" kkkk. Mas é muito boa mesmo! Refinada, equilibrada e com ótimo amargor.' },
  { name: 'Hoegaarden', type: 'Witbier', country: '🇧🇪 Bélgica', abv: 4.9, stars: '⭐⭐⭐⭐⭐', brewery: 'InBev', desc: 'A melhor cerveja de trigo que já provei!! Toque de laranja e coentro. Serve com fatia de laranja!!' },
]
const selectedBeer = ref(null)

// RECEITAS
const recipes = [
  {
    name: 'Frango Caipira na Cerveja',
    emoji: '🍗',
    dificuldade: '⭐⭐ Médio',
    tempo: '1h30min',
    ingredientes: ['1 frango caipira cortado', '2 latas de Brahma Extra', 'Alho, cebola, sal e pimenta a gosto', '2 colheres de manteiga', 'Tomilho e alecrim'],
    preparo: 'Tempere o frango com alho, sal e pimenta e deixe marinar por 1 hora na cerveja. Numa panela grande, derreta a manteiga e doure o frango. Adicione a cerveja da marinada, o tomilho e o alecrim. Cozinhe em fogo baixo por 45 minutos. Sirva com arroz e mandioca frita!!'
  },
  {
    name: 'Bolo de Chocolate com Stout',
    emoji: '🎂',
    dificuldade: '⭐⭐⭐ Difícil',
    tempo: '2 horas',
    ingredientes: ['2 xícaras de farinha', '1 garrafa de Guinness', '200g de chocolate meio amargo', '3 ovos', '1 xícara de açúcar', '100g de manteiga', '1 colher de fermento'],
    preparo: 'Derreta o chocolate com a manteiga em banho-maria. Misture com o açúcar e os ovos. Adicione a cerveja Guinness aos poucos, depois a farinha peneirada e o fermento. Asse em forno médio por 40 minutos. A cerveja deixa o bolo SUPER úmido e gostoso!!'
  },
  {
    name: 'Camarão na Cerveja Pilsen',
    emoji: '🦐',
    dificuldade: '⭐ Fácil',
    tempo: '30 minutos',
    ingredientes: ['500g de camarão limpo', '1 lata de Antarctica', 'Alho, azeite, limão', 'Coentro e pimenta dedo-de-moça', 'Sal a gosto'],
    preparo: 'Refogue o alho no azeite, adicione o camarão e a pimenta. Depois de 5 minutos, despeje a lata de cerveja e deixe reduzir. Finalize com limão e coentro. Sirva com pão francês pra molhar no caldinho!! Simples e delicioso!!'
  },
]

// CURIOSIDADES
const facts = [
  'A cerveja é a terceira bebida mais consumida no mundo, perdendo apenas para a água e o chá!!',
  'A Bíblia menciona cerveja mais de 100 vezes! Os egípcios pagavam os construtores das pirâmides com cerveja!!',
  'A cerveja mais cara do mundo é a "Samichlaus" da Áustria, que custa mais de R$200 a garrafa!',
  'O Brasil é o 4º maior produtor de cerveja do mundo! São mais de 7 bilhões de litros por ano!!',
  'A palavra "toast" (brinde) vem de quando se colocava torrada na cerveja na Idade Média pra melhorar o sabor!!',
  'Estudos científicos mostram que beber cerveja com moderação faz bem pro coração!! (mas não é desculpa pra abusar hein!!)',
  'A cerveja mais antiga conhecida tem mais de 5.000 anos! Foi encontrada na Mesopotâmia!!',
  'No Oktoberfest de 2002, foram consumidos mais de 6 MILHÕES de litros de cerveja em 16 dias!!',
]

const records = [
  { record: 'Maior caneca de chope', holder: 'Munique, Alemanha', value: '15.000 litros' },
  { record: 'Mais rápido a beber 1 litro', holder: 'Bob "Gulão" McFinley (EUA)', value: '1.3 segundos!!' },
  { record: 'Maior coleção de garrafinhas', holder: 'Ronald Zborsky (Polônia)', value: '26.000 garrafas' },
  { record: 'Cerveja mais alcoólica', holder: 'EKU 28 (Alemanha)', value: '11% de álcool' },
  { record: 'Maior fábrica de cerveja', holder: 'AmBev (Brasil)', value: '1.3 bilhão litros/ano' },
]

// FÓRUM
const messages = ref([
  { id: 1, nick: 'BotecoBH', date: '13/03/2003', text: 'Ótimo site!! Uso sempre pra saber as notas das cervejas antes de comprar. Parabéns ao Zé!!' },
  { id: 2, nick: 'Terezonha', date: '11/03/2003', text: 'Fiz o frango na cerveja ontem e ficou DELICIOSO!! Recomendo muito a receita, minha família adorou!!' },
  { id: 3, nick: 'PiracicabaFC', date: '08/03/2003', text: 'A Hoegaarden que vocês avaliaram não encontro em SP, alguém sabe onde vende??' },
  { id: 4, nick: 'Toninho_Chef', date: '05/03/2003', text: 'Oi galera! Sou o Toninho, o chef do site. Em breve terei novas receitas!! Abraços a todos!' },
])
const newMsg = ref({ nick: '', text: '' })
let msgId = 10
function sendMessage() {
  if (!newMsg.value.nick.trim() || !newMsg.value.text.trim()) return
  messages.value.unshift({
    id: msgId++,
    nick: newMsg.value.nick,
    date: new Date().toLocaleDateString('pt-BR'),
    text: newMsg.value.text,
  })
  newMsg.value = { nick: '', text: '' }
}

// SIDEBAR DIREITA
const temp = ref(28)
const tempAdvice = computed(() => temp.value > 30 ? '🔥 Tá quente!! Beba uma gelada!' : '😎 Temperatura ideal pra uma cerveja!')

const currentDate = ref('')
const currentTime = ref('')
function updateTime() {
  const now = new Date()
  currentDate.value = now.toLocaleDateString('pt-BR')
  currentTime.value = now.toLocaleTimeString('pt-BR')
}

// PIADAS
const jokes = [
  'Por que o bebado não joga xadrez? Porque ele sempre toma um bispo!! 😂',
  'O que é um japonês bêbado? Um cara quase de olho fechado!! 🤣',
  'Por que a cerveja tem espuma? Porque se não tivesse seria caldo de cana!! 😆',
  'O que é um pastel de vento acompanhado de cerveja? Uma refeição balanceada!! 😄',
  'Quanto custa uma cerveja zero álcool? Um real. E quanto custa uma cerveja normal? Também um real... mas a zero álcool sai mais cara!! 🤔',
]
const jokeIndex = ref(0)
const currentJoke = computed(() => jokes[jokeIndex.value])
function nextJoke() {
  jokeIndex.value = (jokeIndex.value + 1) % jokes.length
}

// MÚSICA
const songs = [
  { name: 'País Tropical', artist: 'Jorge Ben Jor' },
  { name: 'Aquarela do Brasil', artist: 'Gal Costa' },
  { name: 'Garota de Ipanema', artist: 'Tom Jobim' },
  { name: 'Asa Branca', artist: 'Luiz Gonzaga' },
]
const currentSong = ref(songs[0])

// TICKERS
const tickers = ['Nova receita de churrasco!', 'Avaliação da Devassa Nova', 'Oktoberfest 2003 em breve!', 'Parceria com BarOnline.com.br']

let timer = null
onMounted(() => {
  updateTime()
  timer = setInterval(updateTime, 1000)
  setInterval(() => {
    const idx = Math.floor(Math.random() * songs.length)
    currentSong.value = songs[idx]
  }, 8000)
})
onUnmounted(() => clearInterval(timer))
</script>

<style>
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  background-color: #000033;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='20' height='20'%3E%3Ccircle cx='10' cy='10' r='1' fill='%23003300' opacity='0.4'/%3E%3C/svg%3E");
  font-family: Verdana, Arial, sans-serif;
  font-size: 12px;
  color: #ffdd00;
  min-width: 800px;
}

.body-wrapper {
  max-width: 900px;
  margin: 0 auto;
  background-color: #001a00;
  border: 2px solid #ffdd00;
}

/* MARQUEE */
.marquee-bar {
  background: #ffdd00;
  color: #000;
  font-weight: bold;
  font-size: 13px;
  padding: 2px 0;
  border-bottom: 2px solid #cc9900;
}

/* HEADER */
.header-table { background: linear-gradient(180deg, #003300 0%, #001100 100%); border-bottom: 3px solid #ffdd00; }
.header-left { padding: 10px; }
.logo-emoji { font-size: 48px; display: block; line-height: 1; }
.new-badge { background: #ff0000; color: #fff; font-size: 10px; font-weight: bold; padding: 1px 4px; margin-right: 4px; animation: blink 1s step-end infinite; }
@keyframes blink { 50% { opacity: 0; } }
.site-title { font-size: 36px; font-weight: bold; line-height: 1; }
.title-beer { color: #ffdd00; text-shadow: 2px 2px 0 #cc6600; }
.title-mania { color: #ff6600; text-shadow: 2px 2px 0 #cc3300; }
.title-com { color: #ffaa00; font-size: 20px; }
.site-slogan { color: #aaffaa; font-size: 11px; font-style: italic; margin-top: 4px; }
.header-right { padding: 10px; text-align: right; vertical-align: top; }
.counter-label { font-size: 10px; color: #aaaaaa; }
.counter-digits { display: inline-flex; gap: 1px; margin: 2px 0; }
.digit { background: #000; color: #ff0000; font-family: 'Courier New', monospace; font-weight: bold; font-size: 20px; padding: 2px 5px; border: 1px solid #660000; }
.online-now { color: #00ff00; font-size: 10px; }
.last-update { color: #888; font-size: 10px; }

/* NAVEGAÇÃO */
.nav-table { background: #003300; border-top: 1px solid #ffdd00; border-bottom: 2px solid #ffdd00; }
.nav-item { text-align: center; padding: 0; }
.nav-link { display: block; padding: 6px 4px; color: #ffdd00; text-decoration: none; font-weight: bold; font-size: 11px; white-space: nowrap; }
.nav-link:hover { background: #005500; color: #ffffff; }
.nav-active { background: #ffdd00 !important; color: #000000 !important; }

/* CONTENT TABLE */
.content-table { background: #001a00; }

/* SIDEBAR ESQUERDA */
.sidebar-left { background: #002200; border-right: 2px solid #ffdd00; padding: 8px; }
.sidebar-box { background: #001100; border: 1px solid #556600; padding: 6px; margin-bottom: 8px; }
.sidebar-title { background: #556600; color: #ffdd00; font-weight: bold; font-size: 11px; padding: 2px 4px; margin: -6px -6px 6px -6px; }
.sidebar-list { list-style: none; padding: 0; }
.sidebar-list li { border-bottom: 1px dotted #334400; padding: 2px 0; }
.sidebar-link { color: #aaffaa; text-decoration: none; font-size: 11px; }
.sidebar-link:hover { color: #ffff00; text-decoration: underline; }

/* POLL */
.poll-question { color: #ffffff; font-size: 11px; margin-bottom: 4px; }
.poll-option { margin: 3px 0; font-size: 10px; color: #cccccc; }
.poll-bar-bg { background: #003300; height: 8px; border: 1px solid #446600; margin: 1px 0; }
.poll-bar { background: linear-gradient(90deg, #ffdd00, #ff6600); height: 100%; }
.poll-pct { color: #ffdd00; font-weight: bold; }
.vote-btn { background: #ffdd00; color: #000; border: 1px solid #cc9900; font-size: 10px; padding: 2px 6px; cursor: pointer; margin-top: 4px; font-weight: bold; }
.vote-thanks { color: #00ff00; font-size: 10px; margin-top: 3px; }

/* BANNERS */
.banner-item { background: #003399; color: #fff; border: 1px solid #0066ff; text-align: center; padding: 4px; font-size: 9px; margin-bottom: 2px; }
.banner-item2 { background: #990000; color: #fff; border: 1px solid #ff0000; text-align: center; padding: 4px; font-size: 9px; }

/* MAIN CONTENT */
.main-content { padding: 10px; background: #001a00; }
.section-title { background: linear-gradient(90deg, #004400, #007700); color: #ffdd00; font-weight: bold; font-size: 13px; padding: 4px 8px; margin-bottom: 8px; border-left: 4px solid #ffdd00; border-top: 1px solid #ffdd00; border-bottom: 1px solid #ffdd00; }
.welcome-box { background: #002200; border: 1px solid #446600; padding: 8px; margin-bottom: 10px; color: #ccddcc; line-height: 1.6; }
.welcome-box p { margin-bottom: 6px; }
.intro-text { color: #aaccaa; margin-bottom: 8px; }

/* NEWS */
.news-item { padding: 6px 0; }
.news-date { color: #ff9900; font-size: 10px; font-weight: bold; }
.news-title { color: #ffdd00; font-weight: bold; margin: 2px 0; }
.news-body { color: #ccddcc; line-height: 1.5; }
.hr-dotted { border: none; border-top: 1px dotted #446600; margin: 8px 0; }

/* BEER OF WEEK */
.beer-of-week { background: #002200; border: 2px solid #ffdd00; width: 100%; }
.beer-emoji-cell { font-size: 60px; text-align: center; width: 80px; vertical-align: top; }
.beer-name-big { color: #ffdd00; font-size: 16px; }
.beer-type { color: #aaaaaa; font-size: 11px; }
.rating { color: #ffaa00; font-weight: bold; }

/* CERVEJAS TABLE */
.beers-table { border-collapse: collapse; font-size: 11px; }
.beers-header { background: #ffdd00; color: #000; }
.beers-header th { padding: 4px 6px; text-align: left; }
.row-even { background: #002200; }
.row-odd { background: #001500; }
.row-even td, .row-odd td { padding: 3px 6px; color: #ccddcc; border-bottom: 1px solid #334400; }
.beer-link { color: #ffdd00; text-decoration: none; }
.beer-link:hover { text-decoration: underline; color: #ffffff; }
.beer-detail-box { background: #003300; border: 2px dashed #ffdd00; padding: 10px; margin-top: 12px; }
.beer-detail-title { color: #ffdd00; font-size: 15px; font-weight: bold; margin-bottom: 6px; }
.beer-detail-box p { color: #ccddcc; margin: 3px 0; }
.close-btn { background: #660000; color: #fff; border: 1px solid #ff0000; padding: 2px 8px; cursor: pointer; margin-top: 6px; }

/* RECEITAS */
.recipe-box { background: #002200; border: 1px solid #446600; padding: 8px; margin-bottom: 10px; }
.recipe-title { color: #ffdd00; font-weight: bold; font-size: 14px; margin-bottom: 3px; }
.recipe-meta { color: #888; font-size: 10px; margin-bottom: 6px; }
.recipe-list { padding-left: 16px; color: #ccddcc; margin: 4px 0; }
.recipe-prep { color: #ccddcc; line-height: 1.5; margin-top: 4px; }

/* CURIOSIDADES */
.fact-box { background: #002200; border-left: 3px solid #ffdd00; padding: 6px 8px; margin-bottom: 6px; color: #ccddcc; line-height: 1.5; }
.fact-num { color: #ffdd00; font-weight: bold; }
.records-table { border-collapse: collapse; font-size: 11px; width: 100%; }
.records-table td { padding: 3px 8px; color: #ccddcc; border-bottom: 1px solid #334400; }

/* FÓRUM */
.forum-form { background: #002200; border: 1px solid #446600; padding: 8px; margin-bottom: 10px; }
.form-label { color: #ffdd00; font-weight: bold; font-size: 11px; }
.form-input { background: #001100; color: #fff; border: 1px solid #446600; padding: 3px; font-size: 11px; width: 200px; }
.form-textarea { background: #001100; color: #fff; border: 1px solid #446600; padding: 3px; font-size: 11px; resize: vertical; }
.send-btn { background: #004400; color: #ffdd00; border: 1px solid #ffdd00; padding: 3px 8px; cursor: pointer; font-weight: bold; margin-right: 4px; font-size: 11px; }
.send-btn:hover { background: #006600; }
.clear-btn { background: #440000; color: #ff9900; border: 1px solid #ff6600; padding: 3px 8px; cursor: pointer; font-size: 11px; }
.message-box { background: #002200; border: 1px solid #334400; padding: 6px; margin-bottom: 6px; }
.msg-header { margin-bottom: 3px; }
.msg-nick { color: #ffdd00; font-weight: bold; }
.msg-date { color: #888; font-size: 10px; }
.msg-text { color: #ccddcc; line-height: 1.5; }

/* CONTATO */
.contact-box { background: #002200; border: 1px solid #446600; padding: 10px; margin-bottom: 10px; color: #ccddcc; }
.contact-label { color: #ffdd00; font-weight: bold; font-size: 11px; }
.email-link { color: #00aaff; }
.icq { background: #ffffff; color: #000; padding: 1px 4px; font-weight: bold; font-size: 11px; }
.contact-note { color: #aaffaa; }
.map-fake { background: #111; border: 2px inset #999; color: #888; padding: 20px; text-align: center; font-size: 11px; }

/* SIDEBAR DIREITA */
.sidebar-right { background: #002200; border-left: 2px solid #ffdd00; padding: 8px; }
.temp-display { font-size: 28px; color: #ff6600; font-weight: bold; text-align: center; }
.temp-label { color: #888; font-size: 10px; text-align: center; }
.temp-beer { color: #aaffaa; font-size: 10px; text-align: center; margin-top: 3px; }
.date-display { color: #ffdd00; font-weight: bold; font-size: 12px; text-align: center; }
.time-display { color: #00ff00; font-size: 16px; font-weight: bold; text-align: center; font-family: 'Courier New', monospace; }
.joke-text { color: #ccddcc; font-size: 10px; line-height: 1.4; margin-bottom: 4px; }
.joke-btn { background: #003300; color: #ffdd00; border: 1px solid #ffdd00; font-size: 9px; padding: 1px 4px; cursor: pointer; }
.music-title { color: #ffdd00; font-size: 10px; font-weight: bold; }
.music-artist { color: #aaaaaa; font-size: 10px; }
.music-controls { color: #cccccc; font-size: 10px; margin-top: 4px; }
.ticker-item { color: #aaffaa; font-size: 10px; border-bottom: 1px dotted #334400; padding: 2px 0; }

/* FOOTER */
.footer { background: #000022; border-top: 3px solid #ffdd00; text-align: center; padding: 10px; }
.footer-text { color: #aaaaaa; font-size: 11px; line-height: 1.8; }
.footer-small { font-size: 9px; color: #666; }
.footer-icons { margin: 6px 0; display: flex; justify-content: center; gap: 4px; flex-wrap: wrap; }
.badge { background: #003366; color: #99bbff; border: 1px solid #6699cc; font-size: 9px; padding: 1px 5px; font-weight: bold; }
.footer-hits { color: #ffdd00; font-size: 11px; margin-top: 4px; }
</style>
