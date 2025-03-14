<template>
    <span style="margin-top: -0.2rem">
        <Button @click="postSandboxParameters()" label="Edit in CodeSandbox" class="liveEditorButton" />
    </span>
</template>

<script>
import { services, data } from './LiveEditorData';
export default {
    data() {
        return {
            sandbox_id: null,
            showCodeHighlight: false
        }
    },
    props: {
        name: {
            type: String,
            default: null
        },
        sources: {
            type: Object,
            default: null
        },
        service: {
            type: String,
            default: null
        },
        data: {
            type: String,
            default: null
        },
        components: {
            type: Array,
            default: null
        },
        dependencies: {
            type: String,
            default: null
        },
        extFiles: {
            type: String,
            default: null
        },
        activeButtonIndex: {
            type: String,
            default: null
        },
    },
    methods: {
        postSandboxParameters() {
            fetch('https://codesandbox.io/api/v1/sandboxes/define?json=1', {
                method: "POST",
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                },
                body: JSON.stringify(this.getSandboxParameters())
            })
            .then(response => response.json())
            .then(data => window.open(`https://codesandbox.io/s/${data.sandbox_id}`, '_blank'))
            .catch(() => this.showCodeHighlight = true );
        },

        createSandboxParameters(nameWithExt, files, extDependencies) {

            const dependencies = require('../../../package.json') ? require('../../../package.json').devDependencies : {};

            return {
                files: {
                    'package.json': {
                        content: {
                            main: `src/demo/${nameWithExt}`,
                            dependencies: {
                                ...extDependencies,
                                'vue': dependencies['vue'],
                                'axios': dependencies['axios'],
                                'primevue': '^3.1.1',
                                'primeflex': dependencies['primeflex'],
                                'primeicons': dependencies['primeicons'],
                                '@babel/cli': dependencies['@babel/cli'],
                                '@vue/cli-plugin-babel': dependencies['@vue/cli-plugin-babel'],
                                '@vue/cli-service': dependencies['@vue/cli-service'],
                                '@vue/compiler-sfc': dependencies['@vue/compiler-sfc'],
                                'core-js': dependencies['core-js']
                            },
                        }
                    },
                    'babel.config.js': {
                content: `module.exports = {
    presets: [
        '@vue/cli-plugin-babel/preset'
    ]
}`            
                    },
                    '.eslintrc.js': {
                        content: `module.exports = {
  root: true,
  env: {
    node: true
  },
  'extends': [
    'plugin:vue/vue3-essential',
    'eslint:recommended'
  ],
  parserOptions: {
    parser: 'babel-eslint'
  }
}`
                    },
                    ...files,
                    ...this.extFiles
                }
            }
        },

        getSandboxParameters() {
            let name = this.name;
            let extension = '.vue';
            let extDependencies = this.dependencies || {};
            let content = this.sources.template.content;
            let style = this.sources.template.style || '';
            let scriptText = 'script';
            let _files = {}, components = '', imports = '';

            _files[`src/components/${name}${extension}`] = {       
                content: `${content}
</${scriptText}>

${style}`   
            }

            if(this.components) {
                this.components.forEach(comp => {
                    imports += `import ${comp} from "primevue/${comp.toLowerCase()}";
`;
                    components += `app.component("${comp}", ${comp});
`;
                })
            } else {
                imports = `import ${this.name.slice(0, -4)} from "primevue/${this.name.slice(0, -4).toLowerCase()}";
`;
                components = `app.component("${this.name.slice(0, -4)}", ${this.name.slice(0, -4)});
`;
            }

            _files['src/main.js'] = {
                content: `import { createApp } from "vue";
import "primeflex/primeflex.css";
import "primevue/resources/themes/saga-blue/theme.css";
import "primevue/resources/primevue.min.css";
import "primeicons/primeicons.css";
import App from "./App.vue";
import PrimeVue from "primevue/config";
${imports}
const app = createApp(App);
app.use(PrimeVue, { ripple: true });
${components}
app.mount("#app");
`
            }

            _files['public/index.html'] = {
                content: `<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <link href="https://unpkg.com/primeicons/primeicons.css" rel="stylesheet">
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
`
            }

            _files['src/App.vue'] = {
                content:
`<template>
    <${name}></${name}>
</template>
<${scriptText}>
import ${name} from './components/${name}'
export default {
    components: {
        ${name}
    }
}
</${scriptText}>
<style lang="scss">
@import './App.scss';
</style>
                `
            }

            _files['src/App.scss'] = {
                        content: `html {
    font-size: 14px;
}

body {
    background-color: #ffffff;
    font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Helvetica, Arial, sans-serif, Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol;
    font-weight: normal;
    color: #495057;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    padding: .5em;
    margin-bottom: 50px;
}

h1, h2, h3, h4, h5, h6 {
    margin: 1.5rem 0 1rem 0;
    font-family: inherit;
    font-weight: 600;
    line-height: 1.2;
    color: inherit;
}

h1 { font-size: 2.5rem; }
h2 { font-size: 2rem; }
h3 { font-size: 1.75rem; }
h4 { font-size: 1.5rem; }
h5 { font-size: 1.25rem; }
h6 { font-size: 1rem; }
p {
    line-height: 1.5;
    margin: 0 0 1rem 0;
}

.card {
    margin-bottom: 2rem;
}

input[type="number"] {
    -moz-appearance: textfield;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

@keyframes pulse {
    0% {
        background-color: rgba(165, 165, 165, 0.1)
    }
    50% {
        background-color: rgba(165, 165, 165, 0.3)
    }
    100% {
        background-color: rgba(165, 165, 165, 0.1)
    }
}

.customer-badge {
    border-radius: 2px;
    padding: .25em .5rem;
    text-transform: uppercase;
    font-weight: 700;
    font-size: 12px;
    letter-spacing: .3px;
}

.customer-badge.status-qualified {
    background-color: #C8E6C9;
    color: #256029;
}

.customer-badge.status-unqualified {
    background-color: #FFCDD2;
    color: #C63737;
}

.customer-badge.status-negotiation {
    background-color: #FEEDAF;
    color: #8A5340;
}

.customer-badge.status-new {
    background-color: #B3E5FC;
    color: #23547B;
}

.customer-badge.status-renewal {
    background-color: #ECCFFF;
    color: #694382;
}

.customer-badge.status-proposal {
    background-color: #FFD8B2;
    color: #805B36;
}

.product-badge {
    border-radius: 2px;
    padding: .25em .5rem;
    text-transform: uppercase;
    font-weight: 700;
    font-size: 12px;
    letter-spacing: .3px;
}

.product-badge.status-instock {
    background: #C8E6C9;
    color: #256029;
}

.product-badge.status-outofstock {
    background: #FFCDD2;
    color: #C63737;
}

.product-badge.status-lowstock {
    background: #FEEDAF;
    color: #8A5340;
}

.order-badge {
    border-radius: 2px;
    padding: .25em .5rem;
    text-transform: uppercase;
    font-weight: 700;
    font-size: 12px;
    letter-spacing: .3px;
}

.order-badge.order-delivered {
    background: #C8E6C9;
    color: #256029;
}

.order-badge.order-cancelled {
    background: #FFCDD2;
    color: #C63737;
}

.order-badge.order-pending {
    background: #FEEDAF;
    color: #8A5340;
}

.order-badge.order-returned {
    background: #ECCFFF;
    color: #694382;
}

.image-text {
    vertical-align: middle;
    margin-left: .5rem;
}

.p-multiselect-representative-option {
    display: inline-block;
    vertical-align: middle;
}

.p-multiselect-representative-option img {
    vertical-align: middle;
    width: 24px;
}

.p-multiselect-representative-option span {
    margin-top: .125rem;
}

 .p-column-filter {
    width: 100%;
}

.country-item {
    display: flex;
    align-items: center;
}

.country-item img.flag {
    width: 18px;
    margin-right: .5rem;
}

.flag {
    vertical-align: middle;
}

span.flag {
    width:44px;
    height:30px;
    display:inline-block;
}

img.flag {
    width:30px
}

.layout-content {

    .content-section {
        padding: 2rem;

        &.introduction {
            background-color: #f8f9fa;
            color: #495057;
            padding-bottom: 0;
            display: flex;
            align-items: top;
            justify-content: space-between;
        }

        &.implementation {
            background-color: #f8f9fa;;
            color: #495057;

            +.documentation {
                padding-top: 0;
            }
        }
    }

    .card {
        background: #ffffff;
        padding: 2rem;
        box-shadow: 0 2px 1px -1px rgba(0,0,0,.2), 0 1px 1px 0 rgba(0,0,0,.14), 0 1px 3px 0 rgba(0,0,0,.12);
        border-radius: 4px;
        margin-bottom: 2rem;
    }
}
                        `,
            }

            if (this.service) {
                _files[`src/service/${this.service}.js`] = {
                    content: services[this.service]
                }

                extDependencies['axios'] =  "^0.19.0";
            }

            if (this.data) {
                const dataArr = this.data.split(',');
                dataArr.forEach(el => {
                    _files[`public/data/${el}.json`] = {
                        content: data[el]
                    }
                });
            }

            if(this.name === 'EditorDemo') {
                extDependencies['quill'] =  "^1.3.7";
            }
            if(this.name === 'FullCalendarDemo') {
                extDependencies['@fullcalendar/core'] = "5.4.0";
                extDependencies['@fullcalendar/daygrid'] = "5.4.0";
                extDependencies['@fullcalendar/interaction'] = "5.4.0";
                extDependencies['@fullcalendar/timegrid'] = "5.4.0";
            }

            return this.createSandboxParameters(`${name}${extension}`, _files, extDependencies);
        }
    }
}
</script>