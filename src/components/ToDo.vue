<template>
    <q-layout>
    <!-- Header -->
    <div slot="header" class="toolbar">
      <!-- opens left-side drawer using its ref -->
      <button class="hide-on-drawer-visible" @click="$refs.leftDrawer.open()">
        <i>menu</i>
      </button>
      <q-toolbar-title :padding="1">
        {{title}}
      </q-toolbar-title>
      <!-- opens right-side drawer using its ref -->
      <button class="hide-on-drawer-visible" @click="$refs.rightDrawer.open()">
          <i>menu</i>
        </button>
    </div>
    <!-- Navigation Tabs -->
    <q-tabs slot="navigation">
      <q-tab icon="mail" route="/layout" exact replace>Mails</q-tab>
      <q-tab icon="alarm" route="/layout/alarm" exact replace>Alarms</q-tab>
      <q-tab icon="help" route="/layout/help" exact replace>Help</q-tab>
    </q-tabs>
    <!-- Left-side Drawer -->
    <q-drawer ref="leftDrawer">
      <div class="toolbar">
        <q-toolbar-title>
          Drawer Title
        </q-toolbar-title>
      </div>
      <div class="list no-border platform-delimiter">
        <q-drawer-link icon="mail" :to="{path: '/', exact: true}">
          Link
        </q-drawer-link>
      </div>
    </q-drawer>
    <!-- IF USING subRoutes only: -->
    <router-view class="layout-view"></router-view>
    <!-- OR ELSE, IF NOT USING subRoutes: -->
    <div class="layout-view">
      Hello: <input v-model="title">
      <button @click="add(title)" class="raised rectangle primary" :disabled="title==''"><i>send</i></button>
      <ul>
        <li v-for="td in todos" :key="td">
          {{td.task}} - {{td.user}}
          <button @click="remove(td)"><i>delete</i></button>
        </li>
      </ul>
    </div>
    <!-- Right-side Drawer -->
    <q-drawer ref="rightDrawer" right-side>
      ...
    </q-drawer>
    <!-- Footer -->
    <div slot="footer" class="toolbar">
      ....
    </div>
  </q-layout>
</template>


<script>
import _ from 'lodash'

export default {
  data () {
    return {
      title: 'Hello Batch 7',
      todos: []
    }
  },
  methods: {
    add (ttl) {
      let todo = {
        user: 'Pogi',
        task: ttl
      }
      this.todos.push(todo)
    },
    remove (ttl) {
      let index = _.indexOf(this.todos, ttl)

      this.todos.splice(index, 1)
    }
  }
}
</script>
