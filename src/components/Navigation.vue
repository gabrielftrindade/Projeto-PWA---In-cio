<template>
    <div id="navigation">
        <v-app-bar
        absolute
        elevate-on-scroll
        scroll-target="#scrolling-techniques-7"
        app
        >
            <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
            <v-toolbar-title>{{nomeProjeto}}</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon class="mr-2" @click="homeLink()">
                <v-icon>mdi-home</v-icon>
            </v-btn>
            <v-btn icon class="mr-5" @click="logout()">
                <v-icon>mdi-logout</v-icon>
            </v-btn>
        </v-app-bar>
        <v-navigation-drawer
            v-model="drawer"
            absolute
            temporary
            app
        >
        <v-layout column style="text-align: center">
        <v-flex class="mt-5" >
            <v-avatar
            color="indigo"
            style="text-align: center"
            size="60">
            <span class="white--text text-h5">{{nomeUsuario.substr(0, 1)}}</span>
            </v-avatar>
            <p class="subheading ma-3">Bem Vindo,</p>
            <p class="subheading ma-3">{{nomeUsuario}}</p>
        </v-flex>
        </v-layout>

        <v-divider></v-divider>
        <v-list
            nav
            dense
            rounded
        >
            <v-list-item
                v-for="itemHome in home"
                :key="itemHome.title"
                link
                @click="navegar(itemHome.link)"
            >
                <v-list-item-icon>
                    <v-icon class="material-icons-outlined">{{ itemHome.icon }}</v-icon>
                </v-list-item-icon>

                <v-list-item-content>
                    <v-list-item-title>{{ itemHome.title }}</v-list-item-title>
                </v-list-item-content>

            </v-list-item>
            <div
                v-for="item in opcoes"
                :key="item.principal.title"
            >
                <ul class="pa-0">
                    <v-list-group>
                        <template v-slot:activator>

                            <v-list-item-icon>
                                <v-icon class="material-icons-outlined">{{ item.principal.icon }}</v-icon>
                            </v-list-item-icon>

                            <v-list-item-title
                                link
                            >
                            {{ item.principal.title }}
                            </v-list-item-title>

                        </template>
                        <v-list-item
                            v-for="sub in item.submenus"
                            :key="sub.title"
                            link
                            @click="navegar(sub.link)"
                        >
                            <v-list-item-icon class="pl-4">
                            <v-icon class="material-icons-outlined">{{ sub.icon }}</v-icon>
                            </v-list-item-icon>

                            <v-list-item-content>
                            <v-list-item-title>{{ sub.title }}</v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                    </v-list-group>
                </ul>
            </div>
        </v-list>
        <template v-slot:append>
            <div class="pa-2">
            <v-btn block color="primary" @click="logout()">
                Sair
                <v-icon class="pl-1">mdi-logout</v-icon>
            </v-btn>
            </div>
        </template>
        </v-navigation-drawer>
    </div>
</template>

<script>
export default {
    data: () => ({
        drawer: false,
        group: null,
        nomeProjeto: 'Novo Projeto',
        nomeUsuario: 'Gabriel Ferreira Trindade',
        home: [{ title: 'Página Inicial', link: 'Home', icon: 'mdi-home' }],
        opcoes: [
            {
            principal: {
                title: 'Usuario',
                icon: 'mdi-account'
            },
            submenus: [
                { title: 'Usuario', link: 'Home', icon: 'mdi-account-edit' },
            ]
            }
        ]
    }),
    props: {
        source: String,
    },
    methods: {
        navegar (nome) {
            this.$router.push({ name: nome })
        },
        async logout () {
            this.$router.push({ name: 'Login' })
        },
        homeLink () {
        this.$router.push({ name: 'Home' })
        },
    }
};
</script>