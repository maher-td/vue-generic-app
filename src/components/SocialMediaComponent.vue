<template>
    <section class="social-media">
        <div>
            <a v-clipboard:copy="CopyLink" v-clipboard:success="onCopy">
                <img src="../../src/assets/copy-link.svg" width="25px"/>
            </a>
            <ShareNetwork network="facebook"
                          key="facebook"
                          :url="fullUrl"
                          :title="sharing.title"
                          :description="sharing.description">
                <i class="icon-facebook"></i>
            </ShareNetwork>
            <ShareNetwork network="twitter"
                          key="twitter"
                          :url="shortenUrl"
                          :title="sharing.title"
                          :description="sharing.description"
                          :twitterUser="sharing.twitterUser">
                <i class="icon-twitter"></i>
            </ShareNetwork>
            <ShareNetwork network="whatsapp"
                          key="whatsapp"
                          :url="fullUrl"
                          :title="sharing.title"
                          :description="sharing.description">
                <i class="icon-whatsapp"></i>
            </ShareNetwork>
        </div>

        <!-- <div class="toaster" v-bind:class="{'show-toaster': isToaster}">
            link Copied
        </div> -->
    </section>
</template>

<style lang="scss">
.social-media {
    display: flex;
    justify-content: center;
    padding: 60px;
}
</style>

<script>

    import axios from 'axios';
    import Vue from 'vue';
    import ShareNetwork from 'vue-social-sharing'
    import VueClipboard from 'vue-clipboard2'

    Vue.use(ShareNetwork);
    Vue.use(VueClipboard);

    let socialThis;
    let baseUrl = document.location.origin;
    let apiUrl = baseUrl + "";
    let pageURL = window.location.protocol + "//" + window.location.host + window.location.pathname + window.location.search;

export default {
    data: function() { 
      return {
            CopyLink: pageURL,
            isToaster: false,
            sharing: {
                url: '',
                title: '',
                description: ''
            },
            shortenUrl: "",
            fullUrl: "",
            networks: [
                { network: 'facebook', name: 'Facebook', icon: 'icon-facebook' },
                { network: 'whatsapp', name: 'Whatsapp', icon: 'icon-whatsapp' },
                { network: 'twitter', name: 'Twitter', icon: 'icon-twitter' }
            ]
        }
    },
    methods: {
        onCopy: function () {
            socialThis.isToaster = true;
            setTimeout(() => {
                socialThis.isToaster = false;
            }, 2000);
        }
    },
    computed: {},
    mounted() {
        socialThis = this;
        socialThis.sharing.title = socialThis.socialTitle;
        socialThis.sharing.description = socialThis.socialSummary;

        let pageUrlWithoutSpacing = pageURL.replaceAll("%20", "");

        socialThis.fullUrl = pageURL;

        axios.get(`${apiUrl}/api/tinyurl/index?url=${pageUrlWithoutSpacing}`)
            .then((res) => {
                socialThis.shortenUrl = res.data;
            })
            .catch(() => {
                socialThis.shortenUrl = pageURL;
            })  

    }
}
</script>