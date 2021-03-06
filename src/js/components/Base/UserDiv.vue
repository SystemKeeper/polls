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
	<div class="user-row" :class="type">
		<div v-if="description" class="description">
			{{ description }}
		</div>
		<Avatar :disable-menu="true" :user="userId"
			:is-guest="!Boolean(OC.currentUser)"
			:display-name="computedDisplayName"

			:is-no-user="isNoUser" />
		<div class="avatar" :class="iconClass" />

		<div v-if="!hideNames" class="user-name">
			{{ computedDisplayName }}
		</div>
	</div>
</template>

<script>
import { Avatar } from '@nextcloud/vue'

export default {
	name: 'UserDiv',

	components: {
		Avatar
	},

	props: {
		hideNames: {
			type: Boolean,
			default: false
		},
		userId: {
			type: String,
			default: undefined
		},
		displayName: {
			type: String,
			default: ''
		},
		type: {
			type: String,
			default: 'user'
		},
		description: {
			type: String,
			default: ''
		},
		icon: {
			type: Boolean,
			default: false
		}

	},

	data() {
		return {
			nothidden: false
		}
	},

	computed: {
		isNoUser() {
			return this.type !== 'user'
		},

		isValidUser() {
			return (this.userId)
		},

		iconClass() {
			if (this.icon) {
				if (this.type === 'contact') {
					return 'icon-mail'
				}
				return 'icon-' + this.type
			} else {
				return ''
			}
		},

		computedDisplayName() {
			let value = this.displayName

			if (!this.displayName) {
				if (this.type === 'user') {
					value = this.userId
				} else if (this.type === 'group') {
					value = value + ' (' + t('polls', 'Group') + ')'
				} else {
					value = this.userId
				}
			}
			return value

		}
	}
}

</script>

<style lang="scss">
.user-row {
	display: flex;
	flex: 1;
	align-items: center;
	margin-left: 0;
	margin-top: 0;

	> div {
		margin: 2px 4px;
	}

	.description {
		opacity: 0.7;
		flex: 0;
	}

	.avatar {
		height: 32px;
		width: 32px;
		flex: 0;
	}

	.user-name {
		opacity: 0.5;
		flex: 1;
		overflow: hidden;
		text-overflow: ellipsis;
	}
}
</style>
