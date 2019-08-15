<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <!-- HelloWorld msg="Welcome to Your Vue.js App"/-->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 offset-lg-2">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Pendaftaran</h5>

              <h6 class="card-subtitle mb-2 text-muted">Ayo Join Bersama Kami</h6>

              <div v-if="loading == true">
                <div class="spinner-border" role="status">
                  <span class="sr-only">Loading...</span>
                </div>
              </div>

              <form v-else v-on:submit="submitSignUp" class="text-left">
                <div class="form-group">
                  <label for="exampleInputFullname">Nama Lengkap</label>

                  <input
                    type="text"
                    class="form-control"
                    id="exampleInputFullname"
                    v-model="fullnameForm"
                    placeholder="Masukkan Nama Lengkap"
                  />
                </div>

                <div class="form-group">
                  <label for="exampleInputEmail1">Email</label>

                  <input
                    type="email"
                    class="form-control"
                    id="exampleInputEmail1"
                    aria-describedby="emailHelp"
                    v-model="emailForm"
                    placeholder="Masukkan Email Anda"
                  />

                  <small id="emailHelp" class="form-text text-muted">Email ini rahasia</small>
                </div>

                <div class="form-group">
                  <label for="exampleInputPassword1">Kata Sandi</label>

                  <input
                    type="password"
                    class="form-control"
                    v-model="passwordForm"
                    id="exampleInputPassword1"
                    placeholder="Masukkan Kata Sandi"
                  />
                </div>

                <button type="submit" class="btn btn-primary btn-block">Submit</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
    <hr />

    <component-ortu></component-ortu>
    <hr />
    <h1>{{ pesanBindView }}</h1>

    <hr />

    <input v-bind:placeholder="pesanBindAttribute1" v-model="pesanBindView" />
    <hr />
    <img width="200px" v-bind:src="pesanBindAttribute2" />

    <hr />

    <input v-model="pesanBindDuaArah" />
    <br />
    <h1>{{ pesanBindDuaArah }}</h1>
    <hr />
    <button
      type="button"
      class="btn btn-success mb-2"
      v-on:click="alertBindEvent(pesanBindEvent1)"
    >Klik Aku</button>
    <br />
    <input type="text" placeholder="Input Disini.." v-on:change="alertBindEvent(pesanBindEvent2)" />
    <br />
    <input
      type="text"
      placeholder="Input Disini.."
      v-on:keyup.enter="alertBindEvent(pesanBindEvent3)"
    />
    <hr />Penjumlahan :
    <br />Masukkan angka pertama :
    <input v-model="angkaPertama" />
    <br />Masukkan angka kedua :
    <input v-model="angkaKedua" />
    hasilnya : {{ hasilTambah }}
    <hr />Pengurangan :
    <br />Masukkan angka pertama :
    <input v-model="angkaPertama" />
    <br />Masukkan angka kedua :
    <input v-model="angkaKedua" />
    hasilnya : {{ hasilKurang}}
    <hr />
    <button
      type="button"
      name
      id
      v-on:click="alertAxios()"
      class="btn btn-primary btn-lg btn-block"
    >Tes Klik Axios</button>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import ComponentOrtu from "./components/ComponentOrtu.vue";
import axios from "axios";

export default {
  name: "app",
  components: {
    HelloWorld,
    ComponentOrtu
  },
  data() {
    return {
      pesanBindView: "",
      pesanBindAttribute1: "Silahkan diisi..",
      pesanBindAttribute2:
        "https://banner2.kisspng.com/20180920/rvp/kisspng-javascript-node-js-computer-icons-logo-application-prog-nodejs-svg-png-icon-free-download-437-44-5ba3cfbcdba2b6.0741288815374622048996.jpg",
      pesanBindDuaArah: "Inisiasi Dua Arah",
      pesanBindEvent1: "Event bind dengan click",
      pesanBindEvent2: "Event bind dengan change",
      pesanBindEvent3: "Event bind dengan keyboard",
      angkaPertama: 0,
      angkaKedua: 0,
      angkaHasil: 0,

      responseAPI: ""
    };
  },
  computed: {
    hasilTambah() {
      this.angkaHasil = parseInt(this.angkaPertama) + parseInt(this.angkaKedua);
      return this.angkaHasil;
    },
    hasilKurang() {
      this.angkaHasil = parseInt(this.angkaPertama) - parseInt(this.angkaKedua);
      return this.angkaHasil;
    }
  },
  methods: {
    alertBindEvent(params) {
      alert(params);
    },
    alertAxios(params) {
      axios
        .post("http://proyekagendaapi.herokuapp.com/api/register", {
          name: "isi nama tes axios",
          email: "email@axios.com",
          password: "passwordaxios"
        })
        .then(response => {
          this.responseAPI = response;
          if (response.datastatus == 200) {
            alert("form sukses");
          } else {
            alert("form gagal");
          }
        })
        .catch(error => {
          console.log(error);
          this.errored = error;
        })
        .finally(() => {
          (this.loading = false),
            (this.fullnameForm = ""),
            (this.passwordForm = ""),
            (this.passwordForm = ""),
            (this.emailForm = "");
        });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
