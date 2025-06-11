<!DOCTYPE html>
<html>
<head>
  <title>Escolha seu cachorro</title>
</head>
<body>

  <h2>Escolha a raça e a cor do seu cachorro</h2>

  <select id="raça"></select>
  <select id="cor"></select>

  <p id="descrição"></p>
  <img id="foto" style="max-width:300px; margin-top:10px;" />

  <script>
    // Classe pai
    class Animal {
      constructor(patas, olhos) {
        this.patas = patas
        this.olhos = olhos
      }
    }

    // Cachorro herda de Animal e adiciona mais coisa
    class Cachorro extends Animal {
      constructor(raça, cor, patas, olhos, descrição, foto) {
        super(patas, olhos)
        this.raça = raça
        this.cor = cor
        this.descrição = descrição
        this.foto = foto
      }
    }

    // Nosso “banco” de raças com detalhes e fotos
    const raças = {
      Labrador: {
        patas: 4,
        olhos: 2,
        descrição: "Labrador é amigável, esperto e ótimo companheiro.",
        fotos: {
          Amarelo: "https://cdn.pixabay.com/photo/2017/09/25/13/12/dog-2785074_1280.jpg",
          Preto: "https://cdn.pixabay.com/photo/2017/06/30/18/14/dog-2454713_1280.jpg"
        },
        cores: ["Amarelo", "Preto"]
      },
      Poodle: {
        patas: 4,
        olhos: 2,
        descrição: "Poodle é elegante, brincalhão e super inteligente.",
        fotos: {
          Branco: "https://cdn.pixabay.com/photo/2017/01/23/20/34/poodle-2004177_1280.jpg",
          Marrom: "https://cdn.pixabay.com/photo/2018/01/03/22/39/poodle-3059539_1280.jpg"
        },
        cores: ["Branco", "Marrom"]
      }
    }

    // Pega os selects e os lugares onde vamos mostrar as infos
    const selRaça = document.getElementById('raça')
    const selCor = document.getElementById('cor')
    const descrição = document.getElementById('descrição')
    const foto = document.getElementById('foto')

    // Preenche o select das raças
    function carregaRaças() {
      selRaça.innerHTML = ''
      for(let r in raças) {
        let option = document.createElement('option')
        option.value = r
        option.textContent = r
        selRaça.appendChild(option)
      }
    }

    // Preenche o select das cores de acordo com a raça escolhida
    function carregaCores() {
      let cores = raças[selRaça.value].cores
      selCor.innerHTML = ''
      cores.forEach(cor => {
        let option = document.createElement('option')
        option.value = cor
        option.textContent = cor
        selCor.appendChild(option)
      })
    }

    // Mostra a descrição e a foto certinha
    function mostraInfo() {
      let r = selRaça.value
      let c = selCor.value
      let info = raças[r]
      let dog = new Cachorro(r, c, info.patas, info.olhos, info.descrição, info.fotos[c])

      descrição.textContent = dog.descrição + ` (Patas: ${dog.patas}, Olhos: ${dog.olhos})`
      foto.src = dog.foto
      foto.alt = `${r} ${c}`
    }

    // Quando mudar raça, atualiza cores e info
    selRaça.addEventListener('change', () => {
      carregaCores()
      mostraInfo()
    })

    // Quando mudar cor, só atualiza info
    selCor.addEventListener('change', mostraInfo)

    // Começa carregando as coisas
    carregaRaças()
    carregaCores()
    mostraInfo()

  </script>

</body>
</html>
