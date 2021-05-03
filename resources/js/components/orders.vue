<template>
    <div class="container">
        <div class="justify-content-center d-flex">
            <button
                class="btn btn-sm btn-primary px-2 my-3 mx-2"
                @click="Noveau"
            >
                EN ATTEND
            </button>
            <button
                class="btn btn-sm btn-primary px-2 my-3 mx-2"
                @click="livre"
            >
                LIVRE
            </button>
            <button class="btn btn-sm btn-primary px-2 my-3 mx-2" @click="Tout">
                TOUT
            </button>
        </div>
        <table id="" class=" m-auto mb-8"> 
            <tr>
                <th class="py-1 px-2 bg-green-600 border-green-600 border-l-2  text-white uppercase font-bold text-center text-sm" >name</th>
                <th class="py-1 px-2 bg-green-600  text-white uppercase font-bold text-center text-sm" >description</th>
                <th class="py-1 px-2 bg-green-600  text-white uppercase font-bold text-center text-sm" >ordre par</th>
                <th class="py-1 px-2 bg-green-600  text-white uppercase font-bold text-center text-sm" >date</th>
                <th class="py-1 px-2 bg-green-600 border-green-600 border-r-2  text-white uppercase font-bold text-center text-sm" >statu</th>
            </tr>
            <tr class="py-3 text-center border-b-2 border-green-600 odd:bg-red-300" v-for="order in store.state.all_orders" :key="order[0].id">
                <td class=" border-green-600 border-l-2">{{ order[0].name }}</td>
                <td class=" border-green-600 border-l-2">{{ order[0].description }}</td>
                <td class=" border-green-600 border-l-2">{{ order[1][0].name }}</td>
                <td class=" border-green-600 border-l-2">{{ order[0].created_at }}</td>
                <td class=" border-green-600 border-l-2 border-r-2 ">
                    <button
                        v-if="order[0].statu == 'new'"
                        @click="store.methodes.livred(order[0].id)"
                        class="btn btn-sm btn-danger"
                    >
                        livré
                    </button>
                    <span v-else>Livré</span>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
import { inject, onMounted, ref } from "vue";
export default {
    setup() {
        const store = inject("store");
        onMounted(() => {
            store.methodes.GetAllOrders();
        });
        const orders = ref([]);
        const Noveau = () => {
            console.log("Show only new");
            store.state.all_orders = store.state.all_orders_tool.filter((order) => {
                return order[0].statu == "new";
            });
            console.log("orders = ", orders);
        };
        const livre = () => {
            console.log("Show only livre");
            store.state.all_orders = store.state.all_orders_tool.filter((order) => {
                return order[0].statu == "livre";
            });
            console.log("orders = ", orders);
        };
        const Tout = () => {
            store.state.all_orders = store.state.all_orders_tool;
        };
        return { store, Noveau, livre, Tout, orders };
    },
};
</script>

<style></style>
