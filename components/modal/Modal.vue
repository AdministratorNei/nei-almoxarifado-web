<template>
	<div class="modal fade" tabindex="-1"> 
		<div class="modal-dialog moda-dialog-centered modal-dialog-scrollable"> 
			<div class="modal-content"> 
				<div class="modal-header">
					<slot name="header" />	
				</div>
				<div class="modal-body">
					<slot name="body" />
				</div>
				<div class="modal-footer">
					<slot name="footer" />
				</div>
			</div>
		</div>
	</div>
</template>

<style scoped>
</style>

