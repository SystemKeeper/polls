<!--
  - @copyright Copyright (c) 2018 René Gieling <github@dartcafe.de>
  -
  - @author René Gieling <github@dartcafe.de>
  -
  - @license GNU AGPL version 3 or any later version
  -
  - This program is free software: you can redistribute it and/or modify
  - it under the terms of the GNU Affero General Public License as
  - published by the Free Software Foundation, either version 3 of the
  - License, or (at your option) any later version.
  -
  - This program is distributed in the hope that it will be useful,
  - but WITHOUT ANY WARRANTY; without even the implied warranty of
  - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
  - GNU Affero General Public License for more details.
  -
  - You should have received a copy of the GNU Affero General Public License
  - along with this program.  If not, see <http://www.gnu.org/licenses/>.
  -
  -->

<template>
	<div>
		<SideBarTabDateOptions v-if="acl.allowEdit && poll.type === 'datePoll'" />
		<SideBarTabTextOptions v-if="acl.allowEdit && poll.type === 'textPoll'" />
	</div>
</template>

<script>
import { mapState } from 'vuex'
import SideBarTabDateOptions from './SideBarTabDateOptions'
import SideBarTabTextOptions from './SideBarTabTextOptions'

export default {
	name: 'SideBarTabOptions',

	components: {
		SideBarTabDateOptions,
		SideBarTabTextOptions
	},

	data() {
		return {
			lastOption: '',
			move: {
				step: 1,
				unit: 'week',
				units: ['minute', 'hour', 'day', 'week', 'month', 'year']
			}
		}
	},

	computed: {
		...mapState({
			poll: state => state.poll,
			acl: state => state.acl
		})

	}
}
</script>
