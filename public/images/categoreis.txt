<template>
  <div class="container">
    <table id="categories">
      <tr>
        <th>name</th>
        <th>description</th>
        <th>image</th>
      </tr>

      <tr v-for="category in store.state.categoreis" :key="category.id">
        <td>{{ category.category_name }}</td>
        <td>{{ category.category_description }}</td>
        <td>
          <img
            :src="category.image_url"
            width="60"
            height="60"
            :alt="category.name"
          />
        </td>
      </tr>

      <!-- Button trigger modal -->
      <button
        type="button"
        class="btn btn-primary mt-2"
        data-toggle="modal"
        data-target="#exampleModal"
      >
        Ajouter Catégorie
      </button>
    </table>
  </div>
  <!-- Modal new category -->
  <div
    class="modal fade"
    id="exampleModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Noveau categorie</h5>
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
          <div class="mb-5">
            <form
              class="mb-3"
              @submit="store.methodes.saveNewCategory"
              enctype="multipart/form-data"
            >
              <div class="form-group">
                <label for="formGroupExampleInput">name</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="store.state.new_category.name"
                  id="formGroupExampleInput"
                  placeholder="name"
                />
              </div>
              <div class="form-group">
                <label for="formGroupExampleInput2">description</label>
                <input
                  type="text"
                  class="form-control"
                  id="formGroupExampleInput2"
                  v-model="store.state.new_category.description"
                  placeholder="description"
                />
              </div>
              <div class="form-group" ref="input_image">
                <label for="formGroupExampleInput3">image</label>
                <input
                  type="file"
                  class="form-control"
                  v-on:change="store.methodes.onChange"
                  id="formGroupExampleInput3"
                  ref="image"
                />
              </div>
              <div class="d-flex justify-content-center">
                <img
                  v-if="store.state.new_category.image"
                  style="max-width: 300px"
                  id="picture"
                  src=""
                  alt=""
                />
              </div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-secondary"
                  @click.prevent=""
                  data-dismiss="modal"
                >
                  Quitter
                </button>
                <button
                  type="button"
                  @click="gg"
                  class="btn btn-success"
                  data-dismiss="modal"
                 
                >
                  Enregistrer
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { inject, onMounted, ref, watch } from "vue";
export default {
  setup() {
    const image = ref(null);
    const store = inject("store");
    const input_image = ref(null)
const gg = ()=>{
  console.log('Emm nice');
  store.methodes.saveNewCategory()
  console.log('Emm nice2');
}

    onMounted(() => {
      store.methodes.getCategoreis();
    });

    watch(
      () => store.state.new_category.image,
      () => {
        readURL(image);
        console.log("wata rak tged 3liha ghi4 khdem");
      }
    );
    //this is to show image before sent to database

    function readURL(image) {
      if (image.value.files && image.value.files[0] && store.state.new_category.image) {
        var reader = new FileReader();
        reader.onload = function (e) {
          document
            .getElementById("picture")
            .setAttribute("src", e.target.result);
        };
        reader.readAsDataURL(image.value.files[0]); // convert to base64 string
      }else{
      
        console.log('this is the file',image)
      }
    }
    return { store, image ,gg,input_image};
  },
};
</script>

<style>
#categories {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#categories td,
#categories th {
  border: 1px solid #ddd;
  padding: 8px;
}

#categories tr:nth-child(even) {
  background-color: #f2f2f2;
}

#categories tr:hover {
  background-color: #ddd;
}

#categories th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #4caf50;
  color: white;
}
</style>