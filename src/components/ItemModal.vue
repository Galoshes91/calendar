<template>
    <Modal labelId="RoomCarBooking" size="large" @close="$emit('close')">
        <div class="appointment-config-modal">
            <h2>Room and Car booking</h2>
            <label>I want to book a: </label>
            <Dropdown
                v-bind="itemTypeDrp"
                placeholder="Select type of booking"
                :label-outside="true"
                :searchable="false"
                @option:selected="selectItemType"
                @close="clearItemType"
                v-model="itemTypeDrp.value"
            ></Dropdown>

            <template v-if="itemTypeSelected">
                <h3>{{ itemTypeHeading }}</h3>
            </template>
        </div>
    </Modal>
</template>

<script>
import { NcModal as Modal, NcSelect as Dropdown } from '@nextcloud/vue'

export default {
    name: 'ItemModal',
    components: {
        Modal,
        Dropdown
    },
    data() {
        return {
            itemTypeDrp: {
                options: [
                    'Car',
                    'Room'
                ],
            },
            itemTypeSelected: false,
            itemTypeHeading: ''
        }
    },
    methods: {
        selectItemType(selectedType) {
            this.itemTypeSelected = true
            if(selectedType === 'Car') {
                this.itemTypeHeading = 'Car booking'
            }
            else {
                this.itemTypeHeading = 'Room booking'
            }
        },
        clearItemType() {
            // if the selected value is null, meaning user has cleared it
            if(!this.itemTypeDrp.value) {
                this.itemTypeSelected = false
            }
        }
    },
    props: {}
}
</script>