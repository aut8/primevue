<template>
    <div>
        <div class="content-section introduction">
            <div class="feature-intro">
                <h1>Button</h1>
                <p>Button is an extension to standard button element with icons and theming.</p>
            </div>
        </div>

        <div class="content-section implementation">
            <div class="card">
                <h5>Basic</h5>
                <Button label="Submit" />
                <Button label="Disabled" disabled="disabled" />
                <Button label="Link" class="p-button-link" />

                <h5>Icons</h5>
                <Button icon="pi pi-check" />
                <Button label="Submit" icon="pi pi-check" />
                <Button label="Submit" icon="pi pi-check" iconPos="right" />

                <h5>Compact Icon Buttons</h5>
                <Button class="p-button-compact" label="Submit" icon="pi pi-check" />
                <Button class="p-button-compact" label="Submit" icon="pi pi-check" iconPos="right" />

                <h5>Severities</h5>
                <Button label="Primary" />
                <Button label="Secondary" class="p-button-secondary" />
                <Button label="Success" class="p-button-success" />
                <Button label="Info" class="p-button-info" />
                <Button label="Warning" class="p-button-warning" />
                <Button label="Help" class="p-button-help" />
                <Button label="Danger" class="p-button-danger" />

                <h5>Raised Buttons</h5>
                <Button label="Primary" class="p-button-raised" />
                <Button label="Secondary" class="p-button-raised p-button-secondary" />
                <Button label="Success" class="p-button-raised p-button-success" />
                <Button label="Info" class="p-button-raised p-button-info" />
                <Button label="Warning" class="p-button-raised p-button-warning" />
                <Button label="Help" class="p-button-raised p-button-help" />
                <Button label="Danger" class="p-button-raised p-button-danger" />

                <h5>Rounded Buttons</h5>
                <Button label="Primary" class="p-button-rounded" />
                <Button label="Secondary" class="p-button-rounded p-button-secondary" />
                <Button label="Success" class="p-button-rounded p-button-success" />
                <Button label="Info" class="p-button-rounded p-button-info" />
                <Button label="Warning" class="p-button-rounded p-button-warning" />
                <Button label="Help" class="p-button-rounded p-button-help" />
                <Button label="Danger" class="p-button-rounded p-button-danger" />

                <h5>Text Buttons</h5>
                <Button label="Primary" class="p-button-text" />
                <Button label="Secondary" class="p-button-secondary p-button-text" />
                <Button label="Success" class="p-button-success p-button-text" />
                <Button label="Info" class="p-button-info p-button-text" />
                <Button label="Warning" class="p-button-warning p-button-text" />
                <Button label="Help" class="p-button-help p-button-text" />
                <Button label="Danger" class="p-button-danger p-button-text" />
                <Button label="Plain" class="p-button-text p-button-plain" />

                <h5>Raised Text Buttons</h5>
                <Button label="Primary" class="p-button-raised p-button-text" />
                <Button label="Secondary" class="p-button-raised p-button-secondary p-button-text" />
                <Button label="Success" class="p-button-raised p-button-success p-button-text" />
                <Button label="Info" class="p-button-raised p-button-info p-button-text" />
                <Button label="Warning" class="p-button-raised p-button-warning p-button-text" />
                <Button label="Help" class="p-button-raised p-button-help p-button-text" />
                <Button label="Danger" class="p-button-raised p-button-danger p-button-text" />
                <Button label="Plain" class="p-button-raised p-button-text p-button-plain" />

                <h5>Outlined Buttons</h5>
                <Button label="Primary" class="p-button-outlined" />
                <Button label="Secondary" class="p-button-outlined p-button-secondary" />
                <Button label="Success" class="p-button-outlined p-button-success" />
                <Button label="Info" class="p-button-outlined p-button-info" />
                <Button label="Warning" class="p-button-outlined p-button-warning" />
                <Button label="Help" class="p-button-outlined p-button-help" />
                <Button label="Danger" class="p-button-outlined p-button-danger" />

                <h5>Rounded Icon Buttons</h5>
                <Button icon="pi pi-bookmark" class="p-button-rounded p-button-secondary" />
                <Button icon="pi pi-search" class="p-button-rounded p-button-success" />
                <Button icon="pi pi-user" class="p-button-rounded p-button-info" />
                <Button icon="pi pi-bell" class="p-button-rounded p-button-warning" />
                <Button icon="pi pi-heart" class="p-button-rounded p-button-help" />
                <Button icon="pi pi-times" class="p-button-rounded p-button-danger" />
                <Button icon="pi pi-check" class="p-button-rounded" />

                <h5>Rounded Text Icon Buttons</h5>
                <Button icon="pi pi-check" class="p-button-rounded p-button-text" />
                <Button icon="pi pi-bookmark" class="p-button-rounded p-button-secondary p-button-text" />
                <Button icon="pi pi-search" class="p-button-rounded p-button-success p-button-text" />
                <Button icon="pi pi-user" class="p-button-rounded p-button-info p-button-text" />
                <Button icon="pi pi-bell" class="p-button-rounded p-button-warning p-button-text" />
                <Button icon="pi pi-heart" class="p-button-rounded p-button-help p-button-text" />
                <Button icon="pi pi-times" class="p-button-rounded p-button-danger p-button-text" />
                <Button icon="pi pi-filter" class="p-button-rounded p-button-text p-button-plain" />

                <h5>Rounded and Outlined Icon Buttons</h5>
                <Button icon="pi pi-check" class="p-button-rounded p-button-outlined" />
                <Button icon="pi pi-bookmark" class="p-button-rounded p-button-secondary p-button-outlined" />
                <Button icon="pi pi-search" class="p-button-rounded p-button-success p-button-outlined" />
                <Button icon="pi pi-user" class="p-button-rounded p-button-info p-button-outlined" />
                <Button icon="pi pi-bell" class="p-button-rounded p-button-warning p-button-outlined" />
                <Button icon="pi pi-heart" class="p-button-rounded p-button-help p-button-outlined" />
                <Button icon="pi pi-times" class="p-button-rounded p-button-danger p-button-outlined" />

                <h5>Badges</h5>
                <Button type="button" label="Emails" badge="8" />
                <Button type="button" label="Messages" icon="pi pi-users" class="p-button-warning" badge="8" badgeClass="p-badge-danger" />

                <h5>Button Set</h5>
                <span class="p-buttonset">
                    <Button label="Save" icon="pi pi-check" />
                    <Button label="Delete" icon="pi pi-trash" />
                    <Button label="Cancel" icon="pi pi-times" />
                </span>

                <h5>Sizes</h5>
                <div class="sizes">
                    <Button label="Small" icon="pi pi-check" class="p-button-sm"  />
                    <Button label="Normal" icon="pi pi-check" class="p-button"  />
                    <Button label="Large" icon="pi pi-check" class="p-button-lg" />
                </div>
                <h5>Block Buttons</h5>
                <div class="p-grid">
                    <div class="p-col-12 p-md-3 p-xl-2">
                        <Button class="p-button-block" label="Submit Form" />
                    </div>
                    <div class="p-col-12 p-md-3 p-xl-2">
                        <Button class="p-button-block p-button-secondary p-button-outlined" label="Reset" />
                    </div>
                </div>
            </div>
        </div>

        <ButtonDoc/>
    </div>
</template>

<script>
import ButtonDoc from './ButtonDoc'

export default {
	components: {
		'ButtonDoc': ButtonDoc
    }
}
</script>

<style lang="scss" scoped>
.p-button {
    margin-right: .5rem;
}

.p-buttonset {
    .p-button {
        margin-right: 0;
    }
}

.sizes {
    .button {
        margin-bottom: .5rem;
        display: block;

        &:last-child {
            margin-bottom: 0;
        }
    }
}

@media screen and (max-width: 960px) {
    .p-button {
        margin-bottom: .5rem;

        &:not(.p-button-icon-only) {
            display: flex;
            width: 100%;
        }
    }

    .p-buttonset {
        .p-button {
            margin-bottom: 0;
        }
    }
}
</style>