<template>
    <Modal labelId="RoomCarBooking" size="large" @close="$emit('close')">
        <div class="appointment-config-modal">
            <h2>Girudala room & car booking</h2>
            <label>I want to book a: </label>
            <Dropdown v-bind="itemTypeDrp" placeholder="Select type of booking" :label-outside="true"
                :searchable="false" @option:selected="selectItemType" @close="clearItemType"
                v-model="itemTypeDrp.value"></Dropdown>

            <template v-if="itemTypeSelected">
                <h4>{{ itemTypeHeading }}</h4>

                <p>Select which {{ itemType.toLowerCase() }} you would like to book:</p>
                <Dropdown v-bind="itemBookDrp" placeholder="Select an option..." :label-outside="true"
                    @option:selected="selectItem" @close="clearItem" v-model="itemBookDrp.value"></Dropdown>

                <template v-if="itemSelected">
                    <br /><br />
                    <p>Select when you'd like to book <b>{{ item }}</b></p>
                    <label>From</label>
                    <DatePicker v-model="startTime" type="datetime" :show-second="false" :use12h="true"
                        format="DD/MM/YYYY hh:mma"></DatePicker>
                    <label>Until</label>
                    <DatePicker v-model="endTime" type="datetime" :show-second="false" :use12h="true"
                        format="DD/MM/YYYY hh:mma"></DatePicker>
                </template>
            </template>

            <span class="action-bar">
                <Button>Cancel</Button>
                <!-- TODO: validation. See SaveModel func, then emit if valid-->
                <Button type="primary" :disabled="saveButtonDisabled" @click="$emit('save-booking')">Save</Button>
            </span>
        </div>
    </Modal>
</template>

<script>
import { NcModal as Modal, NcSelect as Dropdown, NcDateTimePicker as DatePicker, NcButton as Button } from '@nextcloud/vue'

export default {
    name: 'ItemModal',
    components: {
        Modal,
        Dropdown,
        DatePicker,
        Button
    },
    data() {
        return {
            itemTypeDrp: {
                options: [
                    'Car',
                    'Room'
                ],
            },
            itemBookDrp: { // TODO: this should be replaced with a call to the DB or something similar to allow a less static list
                options: [
                    'Car/Room1',
                    'Car/Room2',
                    'Car/Room3',
                    'Car/Room4',
                    'Car/Room5',
                    'Car/Room6',
                    'Car/Room7',
                    'Car/Room8',
                    'Car/Room9',
                    'Car/Room0',
                ],
            },
            itemTypeSelected: false,
            itemTypeHeading: '',
            itemType: '',
            item: '',
            itemSelected: false,
            startTime: new Date(),
            endTime: new Date(),
            saveButtonDisabled: true
        }
    },
    methods: {
        selectItemType(selectedType) {
            this.itemTypeSelected = true
            this.itemTypeHeading = `${selectedType} booking`
            this.itemType = selectedType;
        },
        clearItemType() {
            // if the selected value is null, meaning user has cleared it
            if (!this.itemTypeDrp.value) {
                this.itemTypeSelected = false
            }
        },
        selectItem(selectedItem) {
            this.itemSelected = true
            this.item = selectedItem
            this.saveButtonDisabled = false
        },
        clearItem() {
            if (!this.itemBookDrp.value) {
                this.itemSelected = false
                this.saveButtonDisabled = true
            }
        },
        saveModal() { // TODO: validation

        }
    }
}
</script>

<style>
.action-bar {
    display: flex;
    padding-top: 20px;
}
</style>