<template>
  <v-container class="pa-8" fluid>
    <h1 class="h1 text-center">Lista de afazeres</h1>
    <v-form>
      <v-text-field
        label="Nova tarefa"
        v-model="NovaTarefa"
        @keydown.enter="adicionar"
      >
        <v-icon slot="append" @click.enter="adicionar">mdi-send</v-icon>
      </v-text-field>
    </v-form>
    <v-divider></v-divider>

    <v-list color="grey lighten-3" rounded-xl>
      <v-list-item-group>
        <div>
          <v-list-item
            v-for="tarefa of tarefas"
            :key="tarefa.id"
            class="d-flex justify-space-between"
          >
            {{ tarefa.titulo }}
            <v-spacer></v-spacer>
            <v-list-item-action>
              <div class="d-flex flex-columm">
                <div class="mt-1">
                  <v-checkbox class="mt-16" color="red"></v-checkbox>
                </div>
              </div>
            </v-list-item-action>
          </v-list-item>
        </div>
      </v-list-item-group>
    </v-list>
  </v-container>
</template>

<script>
import * as fb from "@/plugins/firebase";
export default {
  data() {
    return {
      uid: "",
      NovaTarefa: "",
      tarefas: [],
    };
  },
  mounted() {
    this.uid = fb.auth.currentUser.uid;
    this.buscarTarefas();
  },

  methods: {
    async buscarTarefas() {
      this.tarefas = [];
      const logTasks = await fb.tasksCollection
        .where("owner", "==", this.uid)
        .get();
      for (const doc of logTasks.docs) {
        this.tarefas.push({
          id: doc.id,
          titulo: doc.data().titulo,
        });
      }
    },
    async adicionar() {
      await fb.tasksCollection.add({
        titulo: this.NovaTarefa,
        dataGravacao: new Date().toISOString().slice(0, 10),
        owner: this.uid,
      });
      this.novaTarefa = "";
      this.buscarTarefas();
    },
  },
};
</script>

<style></style>
