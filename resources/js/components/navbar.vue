<template>
  <nav
    class="bg-gray-50 shadow-md z-10 flex justify-between"
    :class="{
      dark_mode: store.state.active_dark_mode,
      dark_mode_shadow: store.state.active_dark_mode,
    }"
  >
    <a
      class="navbar-brand pl-3 d-flex justify-content-center text-center items-center"
      href="#"
    >
      <img
     
        class="align-middle mx-2"
        src="/assests/logo.png"
        width="50"
        height="50"
        alt=""
      />
      <span
        class="capitalize text-xl text-blue-500 font-bold hidden md:block lg:block xl:block"
        style="font-family: Goblin One"
        >Livraison</span
      >
    </a>
    <div class="flex mr-3 ml-3">
      <div class=" flex justify-center items-center pr-2 pt-1"  >
        <label class="switch">
          <input type="checkbox"  @click="store.methodes.changeMode" />
          <span class="slider round"></span>
        </label>
      </div>
      <div class="mr-1 justify-center items-center flex font-medium">
        <div class="relative">
          <div class="cursor-pointer flex" @click="change_show_langs_panel">
            {{ store.methodes.language("language") }}
            <svg
              class="w-6"
              xmlns="http://www.w3.org/2000/svg"
              className="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="{2}"
                d="M19 9l-7 7-7-7"
              />
            </svg>
          </div>
          <div
            v-if="show_langs_panel"
            class="absolute lang_panel rounded-md overflow-hidden"
            :class="{
              right_50: store.state.language != 'ar',
              left_50: store.state.language == 'ar',
              dark_mode: store.state.active_dark_mode,
              'bg-white': !store.state.active_dark_mode,
            }"
          >
            <div
              @click="chanege_lang('ar')"
              class="flex items-center cursor-pointer hover:bg-gray-600 hover:text-xlg hover:text-gray-200 p-1"
            >
              <img
                class="rounded-sm h-5 w-10"
                src="/assests/arabic_flag.jpg"
                alt=""
              />
              <h3 class="p-2">{{ store.methodes.language("arabic") }}</h3>
            </div>
            <div
              @click="chanege_lang('en')"
              class="flex items-center cursor-pointer hover:bg-gray-600 hover:text-gray-200 p-1 pt-0"
            >
              <img
                class="rounded-sm h-5 w-10"
                src="/assests/american_flag.png"
                alt=""
              />
              <h3 class="p-2">{{ store.methodes.language("english") }}</h3>
            </div>
             <div
              @click="chanege_lang('fr')"
              class="flex items-center cursor-pointer hover:bg-gray-600 hover:text-gray-200 p-1 pt-0"
            >
              <img
                class="rounded-sm h-5 w-10"
                src="/assests/france.jpg"
                alt=""
              />
              <h3 class="p-2">{{ store.methodes.language("french") }}</h3>
            </div>
          </div>
        </div>
      </div>
      <div
        v-if="store.state.userconected || store.state.livreurconected"
        @click="store.methodes.logout"
        class="mr-1 cursor-pointer justify-center items-center hover:text-lg flex font-medium"
      >
        <span>{{ store.methodes.language("logout") }}</span>
        <span
          ><svg
            xmlns="http://www.w3.org/2000/svg"
            class="ml-2 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth="{2}"
              d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"
            /></svg
        ></span>
      </div>
      <div
        v-if="store.state.userconected || store.state.livreurconected"
        class="mr-3 cursor-pointer justify-center items-center hover:text-lg flex font-medium"
      >
        <span
          data-toggle="modal"
          data-target="#profileSettingModal"
          @click="setup_profile_image"
          ><svg
            data-toggle="modal"
            data-target="#exampleModal"
            xmlns="http://www.w3.org/2000/svg"
            class="ml-2 h-6 transform hover:rotate-90 transition ease-in-out"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth="{2}"
              d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"
            />
            <path
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth="{2}"
              d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
            /></svg
        ></span>
      </div>
    </div>
  </nav>

  <!-- Modal -->
  <div
    class="modal fade"
    id="profileSettingModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">
            {{ store.methodes.language("profile_titel") }}
          </h5>
          <button
            type="button"
            class="close"
            data-dismiss="modal"
            aria-label="Close"
          >
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div>
            <div class="flex justify-content-center">
              <div class="relative rounded-full overflow-hidden">
                <img
                  id="picture"
                  class="rounded-full w-52 h-52 cursor-pointer"
                  src="/assests/default_image_user.jpg"
                  alt=""
                />
                <div
                  class="absolute bottom-0 w-full h-10 flex justify-content-center"
                  style="background-color: rgba(0, 0, 0, 0.548)"
                >
                  <span
                    class="text-white font-bold cursor-pointer"
                    @click="click_toChange_profile"
                    >{{
                      store.methodes.language("Change_profile_picture")
                    }}</span
                  >
                  <input
                    @change="Change_profile"
                    type="file"
                    ref="image"
                    hidden="true"
                  />
                </div>
              </div>
            </div>
            <div class="my-3">
              <div class="form-group row">
                <label for="inputphone" class="col-sm-2 col-form-label">{{
                  store.methodes.language("phone")
                }}</label>
                <div class="col-sm-10">
                  <input
                    :value="store.state.the_user['tel']"
                    type="text"
                    class="form-control"
                    id="inputphone"
                  />
                </div>
              </div>
              <div class="form-group row">
                <label for="inputaddress" class="col-sm-2 col-form-label">{{
                  store.methodes.language("address")
                }}</label>
                <div class="col-sm-10">
                  <input
                    :value="store.state.the_user['address']"
                    type="text"
                    class="form-control"
                    id="inputaddress"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">
            {{ store.methodes.language("close") }}
          </button>
          <button type="button" class="btn btn-primary">
            {{ store.methodes.language("save") }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { inject, ref } from "vue";

export default {
  setup() {
    const show_langs_panel = ref(false);
    const store = inject("store");
    const image = ref(null);
    const profile_image = ref(null);

    const click_toChange_profile = () => {
      image.value.click();
    };
    function Change_profile() {
      console.log("image profile changed");
      if (image.value.value) {
        let validExtensions = ["image/jpeg", "image/jpg", "image/png"];
        if (!validExtensions.includes(image._value.files[0].type)) {
          console.log("This is not a picture");
        } else {
          readURL(image);
          store.state.new_profile_img = image.value.files[0];
          store.methodes.saveImageprofile();
          console.log("profile should be updated");
        }
      }
    }

    const readURL = (image) => {
      var reader = new FileReader();
      reader.readAsDataURL(image.value.files[0]); // convert to base64 string
      reader.onload = function (e) {
        document.getElementById("picture").setAttribute("src", e.target.result);
      };
    };

    function chanege_lang(lang_code) {
      store.state.language = lang_code;
      if (store.state.language == "en") {
        document.getElementById("html").setAttribute("lang", store.state.language);
        document.getElementById("html").classList.remove("arabic");
      } else if (store.state.language == "ar") {
        document.getElementById("html").classList.add("arabic");
        document.getElementById("html").setAttribute("lang", store.state.language);
      }else if (store.state.language == "fr") {
        document.getElementById("html").classList.remove("arabic");
        document.getElementById("html").setAttribute("lang", store.state.language);
      }

      show_langs_panel.value = false;
    }

    function change_show_langs_panel() {
      show_langs_panel.value = !show_langs_panel.value;
    }
    function setup_profile_image() {
      if (store.state.the_user["profile_img"] == null) {
        document
          .getElementById("picture")
          .setAttribute("src", "/assests/default_image_user.jpg");
      } else {
        document
          .getElementById("picture")
          .setAttribute("src", store.state.the_user["profile_img"]);
      }
    }
    return {
      store,
      Change_profile,
      click_toChange_profile,
      readURL,
      image,
      profile_image,
      setup_profile_image,
      chanege_lang,
      show_langs_panel,
      change_show_langs_panel,
    };
  },
};
</script>
 
<style>
.nav-link {
  cursor: pointer;
}
@media only screen and (max-width: 600px) {
  .navnav {
    margin-left: 45vw;
  }
}
@media only screen and (min-width: 601px) {
  .navnav {
    margin-left: 47vw;
  }
}
@media only screen and (min-width: 992px) {
  .navnav {
    margin-left: 75vw;
  }
  .bg-changer {
    background-color: rgba(0, 0, 0, 0.548);
  }
}
.lang_panel {
  -webkit-box-shadow: 0px 0px 16px 3px rgba(0, 0, 0, 0.49);
  box-shadow: 0px 0px 16px 3px rgba(0, 0, 0, 0.49);
  width: max-content;
  z-index: 4000;
}
.right_50 {
  right: 50px;
}
.left_50 {
  left: 50px;
}
.dark_mode {
  color: rgb(230, 230, 230);
  background-color: rgb(48, 48, 48);
}
.dark_mode_shadow {
  -webkit-box-shadow: 0px 0px 16px 3px rgba(124, 124, 124, 0.49);
  box-shadow: 0px 0px 16px 3px rgba(124, 124, 124, 0.49);
  position: relative;
}
.switch {
  position: relative;
  display: inline-block;
  width: 30px;
  height: 17px;
}


.switch input { 
  opacity: 0;
  width: 0;
  height: 0;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 13px;
  width: 13px;
  left: 2px;
  bottom: 2px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(13px);
  -ms-transform: translateX(13px);
  transform: translateX(13px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 17px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>
