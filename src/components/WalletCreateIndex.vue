<template>
    <div class="page-group">
        <div class="page" id="page-wallet-empty">
            <div class="content">
                <div class="center-content">
                    <div class="content-block">
                        <p>
                            <i class="gxicon gxicon-bind"></i>
                        </p>
                        <p class="text-bind">{{$t('wallet_create.index.tip_empty')}}</p>
                    </div>
                    <div class="content-block block-button">
                        <p>
                            <router-link :to="link('/wallet-import',{from:$route.fullPath})" class="button button-idac-secondary">
                                {{$t('wallet_create.index.button_import')}}
                            </router-link>
                        </p>
                        <p>
                            <router-link :to="link('/wallet-create-step-1',{from:$route.fullPath})" class="button button-idac">
                                {{$t('wallet_create.index.button_create')}}
                            </router-link>
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import {
        mapGetters
    } from 'vuex';
    import {
        get_wallets
    } from '@/services/WalletService';

    export default {
        methods: {
            loadWallets () {
                if (get_wallets().length > 0) {
                    this.$router.replace({
                        path: this.link('/')
                    });
                }
            },
            switchLanguage () {
                this.$i18n.locale = 'zh-CN';
            }
        },
        mounted () {
            $.init();
            this.loadWallets();
            if (this.isNative) {
                window.webview = {
                    reload: () => {
                        this.loadWallets();
                    }
                };
            }
        },
        computed: {
            ...mapGetters({
                isNative: 'isNative'
            }),
            imgFlag () {
                let locale = this._i18n.locale.split('-')[1];
                return `static/img/${locale.toUpperCase()}.png`;
            }
        }
    };
</script>
<style scoped lang="scss">
    .content {
        background: #3d4145;
    }

    .center-content {
        margin-top: 3rem;
        flex-direction: column;
        align-items: flex-end;
        display: flex;
        justify-content: center;
        text-align: center;
        .gxicon-bind {
            font-size: 6.5rem;
            color: #d5d5d5;
        }
        .text-bind {
            font-size: .75rem;
        }
        .content-block {
            width: 100%;
        }
        .text-success {
            margin-top: 1.5rem;
        }
        .block-button {
            padding: 0 2rem;
            margin-top: 1rem;
            letter-spacing: .15rem;
        }
    }
</style>
