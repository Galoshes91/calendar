<!--
  - SPDX-FileCopyrightText: 2019 Nextcloud GmbH and Nextcloud contributors
  - SPDX-License-Identifier: AGPL-3.0-or-later
-->

<template>
	<div>
		<NcAppNavigationCaption class="app-navigation-entry-new-calendar"
			:class="{'app-navigation-entry-new-calendar--open': isOpen}"
			:name="$t('calendar', 'Calendars')"
			:menu-open.sync="isOpen"
			@click.prevent.stop="toggleDialog">
			<template #actionsTriggerIcon>
				<Plus :size="20" :title="$t('calendar', 'Add new')" decorative />
			</template>
		</NcAppNavigationCaption>
		<PublicCalendarSubscriptionPicker v-if="showHolidaySubscriptionPicker"
			:show-holidays="true"
			@close="showHolidaySubscriptionPicker = false" />
		<PublicCalendarSubscriptionPicker v-if="showPublicCalendarSubscriptionPicker"
			@close="showPublicCalendarSubscriptionPicker = false" />
	</div>
</template>

<script>
import {
	NcActionButton as ActionButton,
	NcActionInput as ActionInput,
	NcActionSeparator as ActionSeparator,
	NcActionText as ActionText,
	NcAppNavigationCaption,
} from '@nextcloud/vue'
import {
	showError,
} from '@nextcloud/dialogs'

import { uidToHexColor } from '../../../utils/color.js'

import CalendarBlank from 'vue-material-design-icons/CalendarBlank.vue'
import CalendarCheck from 'vue-material-design-icons/CalendarCheck.vue'
import LinkVariant from 'vue-material-design-icons/LinkVariant.vue'
import Plus from 'vue-material-design-icons/Plus.vue'
import Web from 'vue-material-design-icons/Web.vue'
import { mapStores, mapState } from 'pinia'
import useCalendarsStore from '../../../store/calendars.js'
import useSettingsStore from '../../../store/settings.js'

export default {
	name: 'CalendarListNew',
	components: {
		ActionButton,
		ActionInput,
		ActionSeparator,
		ActionText,
		NcAppNavigationCaption,
		CalendarBlank,
		CalendarCheck,
		PublicCalendarSubscriptionPicker: () => import(/* webpackChunkName: "public-calendar-subscription-picker" */ '../../Subscription/PublicCalendarSubscriptionPicker.vue'),
		LinkVariant,
		Plus,
		Web,
	},
	data() {
		return {
			// Open state
			isOpen: false,
			// New subscription
			showHolidaySubscriptionPicker: false,
			showPublicCalendarSubscriptionPicker: false,
		}
	},
	computed: {
		...mapState(useSettingsStore, {
			canSubscribeLink: 'canSubscribeLink',
			hasPublicCalendars: store => Boolean(store.publicCalendars),
		}),
		...mapStores(useCalendarsStore),
	},
	watch: {
		isOpen() {
			if (this.isOpen) {
				return
			}

			this.closeMenu()
		},
	},
	methods: {
		/**
		 * Opens the Actions menu when clicking on the main item label
		 */
		toggleDialog() {
			this.isOpen = !this.isOpen
		},
	},
}
</script>

<style scoped>
:deep(.action-item__menutoggle) {
	opacity: 1 !important;
}
</style>
