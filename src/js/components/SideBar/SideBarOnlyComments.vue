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
	<AppSidebar ref="sideBar" :title="t('polls', 'Details')" @close="$emit('closeSideBar')">
		<UserDiv slot="primary-actions" :user-id="poll.owner" :description="t('polls', 'Owner')" />

		<AppSidebarTab :name="t('polls', 'Comments')" icon="icon-comment">
			<Comments />
		</AppSidebarTab>
	</AppSidebar>
</template>

<script>
import { AppSidebar, AppSidebarTab } from '@nextcloud/vue'

import Comments from '../Comments/Comments'
import { mapState } from 'vuex'

export default {
	name: 'SideBarOnlyComments',
	components: {
		Comments,
		AppSidebar,
		AppSidebarTab
	},

	computed: {
		...mapState({
			poll: state => state.poll,
			acl: state => state.acl
		})
	}

}

</script>

<style scoped lang="scss">

	ul {
		& > li {
			margin-bottom: 30px;
			& > .comment-item {
				display: flex;
				align-items: center;

				& > .date {
					right: 0;
					top: 5px;
					opacity: 0.5;
				}
			}
			& > .message {
				margin-left: 44px;
				flex: 1 1;
			}
		}
	}
</style>
