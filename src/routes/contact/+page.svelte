<script>
	import { fade } from 'svelte/transition';
	import { enhance } from '$app/forms';
	import { imask } from 'svelte-imask';
	const maskConfig = { mask: '(000) 000-0000' };

	let formData = {
		name: '',
		email: '',
		phone: '',
		service: '',
		message: ''
	};

	let status = {
		submitting: false,
		message: '',
		success: false
	};

	function handleSubmit() {
		status.submitting = true;
		return async ({ result }) => {
			status.submitting = false;
			if (result.type === 'success') {
				status.success = true;
				status.message = result.data.message;
				// Reset form on success
				formData = {
					name: '',
					email: '',
					phone: '',
					service: '',
					message: ''
				};
				setTimeout(() => {
					status.success = false;
					status.message = '';
				}, 5000);
			} else {
				status.success = false;
				status.message = 'There was an error sending your message. Please try again.';
				setTimeout(() => {
					status.message = '';
				}, 2500);
			}
		};
	}
</script>

<div class="contactPage">
	<div class="container">
		<h1 class="pageTitle">Contact Us</h1>
		{#if status.message}
			<div
				class="alert"
				class:success={status.success}
				class:error={!status.success}
				transition:fade
			>
				{status.message}
			</div>
		{/if}

		<form method="POST" use:enhance={handleSubmit} class="contactForm">
			<div class="formGroup">
				<label for="name">Name</label>
				<input type="text" id="name" name="name" bind:value={formData.name} required />
			</div>

			<div class="formGroup">
				<label for="email">Email</label>
				<input type="email" id="email" name="email" bind:value={formData.email} required />
			</div>

			<div class="formGroup">
				<label for="phone">Phone (optional)</label>
				<input
					type="tel"
					id="phone"
					name="phone"
					use:imask={maskConfig}
					bind:value={formData.phone}
				/>
			</div>
			<div class="formGroup">
				<label for="service">Services Needed</label>
				<select id="service" name="service">
					<option value="" disabled selected>Select Service</option>
					<option value="dj">DJ</option>
					<option value="photobooth">Photo Booth</option>
					<option value="both dj and photobooth">Both</option>
				</select>
			</div>

			<div class="formGroup">
				<label for="message">Message</label>
				<textarea id="message" name="message" bind:value={formData.message} rows="5" required
				></textarea>
			</div>

			<button type="submit" class="submitButton" disabled={status.submitting}>
				{status.submitting ? 'Sending...' : 'Send Message'}
			</button>
		</form>
	</div>
</div>

<style>
	.contactForm {
		display: flex;
		flex-direction: column;
		gap: 1rem;
		max-width: 700px;
		margin: 0 auto;
	}

	input {
		margin-bottom: 1.2rem;
	}

	.formGroup {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}
	.submitButton {
		display: flex;
		justify-content: center;
		align-items: center;
		background: linear-gradient(to right bottom, rgba(0, 0, 0, 0.85), rgba(0, 0, 0, 0.65));
		color: var(--background);
		border: none;
		padding: 0.5rem 1rem;
		border-radius: 0.25rem;
		width: 250px;
		aspect-ratio: 5 / 1.5;
		border-radius: 100px;
		border: 3px solid #fff;
		margin: 3rem auto 0;
		transition: box-shadow 0.3s ease;
		cursor: pointer;
		&:hover {
			box-shadow: 0 0 2rem 0 rgba(255, 255, 255, 0.75);
		}
	}
	input,
	textarea {
		font-size: 1.6rem;
		padding: 0.5rem 1rem;
	}
</style>
