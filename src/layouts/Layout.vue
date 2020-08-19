<template>
    <q-layout view="hHh LpR fFf">
        <q-header elevated>
            <q-toolbar>
                <q-toolbar-title class="absolute-center">
                    Lista de Tarefas
                </q-toolbar-title>
            </q-toolbar>
        </q-header>

        <q-footer class="footer-index">
            <q-tabs>
                <q-route-tab v-for="(link, index) in essentialLinks"
                             :key="index" :icon="link.icon" :label="link.title" :to="link.link"></q-route-tab>
            </q-tabs>
        </q-footer>

        <q-drawer
                v-model="leftDrawerOpen"
                :breakpoint="767"
                :width="250"
                show-if-above
                bordered
                content-class="bg-primary"
        >
            <q-list dark>
                <q-item-label
                        header
                >
                    Navigation
                </q-item-label>
                <EssentialLink
                        v-for="link in essentialLinks"
                        :key="link.title"
                        v-bind="link"
                        class="text-grey-4"
                />
            </q-list>
        </q-drawer>

        <q-page-container>
            <router-view></router-view>
        </q-page-container>
    </q-layout>
</template>

<script>
    import EssentialLink from 'components/EssentialLink.vue'

    const linksData = [
        {
            title: 'Tarefas',
            icon: 'list',
            link: '/'
        },
        {
            title: 'Configurações',
            icon: 'settings',
            link: '/settings'
        }
    ];

    export default {
        name: 'Layout',
        components: {EssentialLink},
        data() {
            return {
                leftDrawerOpen: false,
                essentialLinks: linksData
            }
        }
    }
</script>
<style lang="scss">
    @media screen and (min-width: 768px) {

        .q-footer {
            display: none;
        }
    }

    .q-drawer {

        .q-router-link--exact-active {
            color: white !important;
        }

    }
    .footer-index{
        z-index: 10 !important;
    }

</style>
