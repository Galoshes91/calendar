<template>
    <div>
        <AppNavigationCaption class="appointment-config-list__caption" 
            :name="'Room & Car booking system'">
            <template #actions>
                <ActionButton :close-after-click="true"
                    @click="showModal = true">
                    <template #icon>
                        <PlusIcon :size="20" decorative />
                    </template>
                </ActionButton>
            </template>
        </AppNavigationCaption>
    
        <ItemModal 
            v-if="showModal"
            @close="closeModal"
        ></ItemModal>
    </div>
</template>

<script>

import {
	NcAppNavigationCaption as AppNavigationCaption,
    NcActionButton as ActionButton,
} from '@nextcloud/vue'
import PlusIcon from 'vue-material-design-icons/Plus.vue'
import ItemModal from '../ItemModal.vue'

export default {
    name: 'ItemBookingList',
    components: {
        AppNavigationCaption,
        ActionButton,
        ItemModal,
        PlusIcon
    },
    data() {
        return {
            showModal: false,
        }
    },
    methods: {
        closeModal() {
            this.showModal = false
        }
    }
}
</script>
