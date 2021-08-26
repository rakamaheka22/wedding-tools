<template>
  <div>
    <h1>List Wedding Invitation Muthia & Raka</h1>
    <div class="invitation">
      <input v-model="payload.nama" type="text" class="inputfield" placeholder="Nama: (Contoh: Raka Maheka)">
      <br />
      <input v-model="payload.telp" type="text" class="inputfield" placeholder="No Telp: (Contoh: 085798291910)">
      <br />
      <select v-model="payload.sesi">
        <option value="" selected>Pilih Sesi</option>
        <option value="SESI1">Sesi 1</option>
        <option value="SESI2">Sesi 2</option>
      </select>
      <br />
      <button @click="addRow">Buat Undangan</button>
    </div>
    <div class="tab">
      <button @click="fetchData('SESI1')">SESI 1</button>
      <button @click="fetchData('SESI2')">SESI 2</button>
    </div>
    <ul>
      <li v-for="(items, index) in listInvite" :key="index" :style="!items.link ? 'background: #ffec9e' : ''">
        <div class="flex">
          <div>
            {{ items.nama }}
            <div style="margin-top: 5px">
              <span :class="items.status === 'TRUE' ? 'green' : 'red'">
                {{ items.status === 'TRUE' ? 'Sudah dishare' : 'Belum dishare' }}
              </span>
            </div>
          </div>
          <div class="sharing">
            <button class="wa" @click="shareSocial(items.id, items.link, items.telp, items.nama, 'wa')">WA</button>
            <button class="tele" @click="shareSocial(items.id, items.link, items.telp, items.nama, 'tele')">Tele</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

const BASE_URL = 'https://api.steinhq.com/v1/storages/61271ceb47873c2b733d6dab';

export default {
  name: 'App',
  data() {
    return {
      listInvite: [],
      sesi: 'SESI1',
      payload: {
        nama: '',
        telp: '',
        sesi: ''
      }
    }
  },
  mounted() {
    this.fetchData('SESI1');
  },
  methods: {
    fetchData(type) {
      this.sesi = type;
      axios.get(`${BASE_URL}/${type}`).then(res => this.listInvite = res.data);
    },
    shareSocial(id, link, telp, name, type) {
      const schedule = this.sesi === 'SESI1' ? 'Sesi 1: Pukul 11.00-13.00' : 'Sesi 2: Pukul 13.00-14.00';


      const descTele = `
🌿🍀🍀🍀🍀🍀🍀🍀🍀🌿

Kepada Yth.
Bapak/Ibu/Saudara/i

**${name}**
__________

بسم اللّه الرحمن الرحمن الر حيم
__Assalamu’alaikum Warahmatullaahi Wabarakaatuh__


__"Dan di antara tanda-tanda (kebesaran)-Nya ialah Dia menciptakan pasangan-pasangan untukmu dari jenismu sendiri, agar kamu cenderung dan merasa tenteram kepadanya, dan Dia menjadikan di antaramu rasa kasih dan sayang. Sungguh, pada yang demikian itu benar-benar terdapat tanda-tanda (kebesaran Allah) bagi kaum yang berpikir."__
(QS. Ar-Ruum: 21)

Dengan memohon Ridho serta Rahmat dari Allah SWT, serta mengamalkan Sunnah Rasulullah SAW, kami bermaksud mengundang Bapak/Ibu/Saudara/i sekalian untuk menghadiri acara Walimatul 'Urs putra-putri kami yang InsyaAllah akan dilaksanakan pada:

🗓️ **Ahad, 5 September 2021**
🕙 Sesi 1 : Pukul 11.00-13.00
🕛 Sesi 2 : Pukul 13.00-14.00
🏢 Bertempat di Gedung Aulia Hall Center (google map terdapat pada link)

${link}

Sehubungan dengan kondisi pandemi Covid-19 saat ini dan mengikuti protokol kesehatan, kami meminta maaf yang sebesar-besarnya kepada Bapak/Ibu/Saudara/i untuk berkenan **menghadiri acara kami pada jam yang telah tercantum di bawah.**

__Jazaakumullah khayran katsiiran__
Terimakasih atas perhatiannya.
Wassalamu'alaikum Warahmatullahi Wabarakaatuh

**Kami yang berbahagia,**
Muthia dan Raka
__________
**Dimohon Bapak/Ibu/Saudara/i hadir pada acara ${schedule}**
`;

      const descWA = `
🌿🍀🍀🍀🍀🍀🍀🍀🍀🌿

Kepada Yth.
Bapak/Ibu/Saudara/i

*${name}*
__________

بسم اللّه الرحمن الرحمن الر حيم
_Assalamu’alaikum Warahmatullaahi Wabarakaatuh_


_"Dan di antara tanda-tanda (kebesaran)-Nya ialah Dia menciptakan pasangan-pasangan untukmu dari jenismu sendiri, agar kamu cenderung dan merasa tenteram kepadanya, dan Dia menjadikan di antaramu rasa kasih dan sayang. Sungguh, pada yang demikian itu benar-benar terdapat tanda-tanda (kebesaran Allah) bagi kaum yang berpikir."_
(QS. Ar-Ruum: 21)

Dengan memohon Ridho serta Rahmat dari Allah SWT, serta mengamalkan Sunnah Rasulullah SAW, kami bermaksud mengundang Bapak/Ibu/Saudara/i sekalian untuk menghadiri acara Walimatul 'Urs putra-putri kami yang InsyaAllah akan dilaksanakan pada:

🗓️ *Ahad, 5 September 2021*
🕙 Sesi 1 : Pukul 11.00-13.00
🕛 Sesi 2 : Pukul 13.00-14.00
🏢 Bertempat di Gedung Aulia Hall Center (google map terdapat pada link)

${link}

Sehubungan dengan kondisi pandemi Covid-19 saat ini dan mengikuti protokol kesehatan, kami meminta maaf yang sebesar-besarnya kepada Bapak/Ibu/Saudara/i untuk berkenan _*menghadiri acara kami pada jam yang telah tercantum di bawah.*_

_Jazaakumullah khayran katsiiran_
Terimakasih atas perhatiannya.
Wassalamu'alaikum Warahmatullahi Wabarakaatuh

_*Kami yang berbahagia,*_
Muthia dan Raka
__________
_*Dimohon Bapak/Ibu/Saudara/i hadir pada acara ${schedule}*_
`;


      let phoneNumber = '';

      if (telp && telp !== 'Grup') {
          const newtelp = telp.replaceAll('-', '');
          phoneNumber = this.convertPhoneNumberWithoutPlus(newtelp);
      }

      switch (type) {
        case 'wa':

          axios.put(`${BASE_URL}/${this.sesi}`, {
            condition: {
              id
            },
            set: {
              status: 'TRUE'
            }
          }).then(res => console.log(res.data));

          if (phoneNumber) {
            window.open(`https://wa.me/${phoneNumber}?text=${encodeURI(descWA)}`);
          } else {
            window.open(`https://wa.me/?text=${encodeURI(descWA)}`);
          }

          break;
        case 'tele':

          window.open(`tg://msg?text=${encodeURI(descTele)}`);
          
          break;
      
        default:
          break;
      }
    },
    async addRow() {
      if (this.payload.nama) {

        const nama = this.payload.nama.replace('&', 'dan');

        const req = [
          {
            id: this.payload.nama.substring(0, 3) + Math.floor(100000 + Math.random() * 900000),
            nama,
            link: `https://muthiaraka.weddingwish.id/?name=${encodeURI(nama)}`,
            telp: this.payload.telp,
            status: 'FALSE'
          }
        ];

        axios.post(`${BASE_URL}/${this.payload.sesi}`, req).then(() => location.reload());
      }
    },
    convertPhoneNumberWithoutPlus(phone) {
      let phoneNumber = phone.toString()
      if (phoneNumber.startsWith('08')) {
        const newphone = phoneNumber.substring(1)
        phoneNumber = `62${newphone}`
        return phoneNumber
      }
      if (phoneNumber.startsWith('8')) {
        phoneNumber = `62${phoneNumber}`
        return phoneNumber
      }
      return null
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  margin: 10px 10px 30px 10px;
}

.tab {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.tab button {
  border: 1px solid #2c3e50;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

li {
  padding: 24px 16px;
  border-radius: 10px;
  background: #f7f4f1;
  margin: 10px;
  font-weight: bold;
}

li:hover, li:hover .green, li:hover .red {
  background: #1f7ae5;
  color: white;
}

li span {
  font-size: 12px;
}

.green {
  color: green;
}

.red {
  color: red  ;
}

.flex {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.sharing {
  margin: 20px 0px 10px 0px;
  display: flex;
  align-items: center;
  justify-content: center;

}

button {
  border: none;
  padding: 10px 24px;
  border-radius: 10px;
  background: white;
  margin: 0px 10px;
  font-weight: bold;
}

.wa {
  color: #28aa7e;
}

.wa:hover {
  color: white;
  background: #28aa7e;
}

.ig {
  color: #991fd6;
}

.ig:hover {
  color: white;
  background: #991fd6;
}

.tele {
  color: #13acff;
}

.tele:hover {
  color: white;
  background: #13acff;
}

.invitation {
  margin: 16px 10px;
}

.invitation input, .invitation select {
  min-width: 300px;
  border: 1px solid #2c3e50;
  padding: 10px;
  border-radius: 10px;
  margin: 10px 0px;
}

.invitation button {
  background: #1f7ae5;
  color: white;
  margin: 10px 0px;
}

.invitation button:hover {
  background: white;
  color: #1f7ae5;
}

</style>
