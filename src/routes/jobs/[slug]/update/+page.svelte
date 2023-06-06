<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { getUserId } from '../../../../utils/auth.js';
    import { goto } from '$app/navigation';
    import { getTokenFromLocalStorage } from '../../../../utils/auth.js';

    export let data;
    let formErrors = {};

    async function updateJob(evt) {
		evt.preventDefault();
		
		const updateJobData = {
            user: getUserId(),
			title: evt.target['title'].value,
			minAnnualCompensation: evt.target['minAnnualCompensation'].value,
			maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
			description: evt.target['description'].value,
			requirements: evt.target['requirements'].value,
			applicationInstructions: evt.target['applicationInstructions'].value,
			location: evt.target['location'].value,
			employer: evt.target['employer'].value
		};

		const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records/' + `${data.job.id}`, 
        {
        method: 'PATCH',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json',
          Authorization : getTokenFromLocalStorage()
        },
        body: JSON.stringify(updateJobData)
      });
  
        if (resp.status == 200) {
            goto ('/jobs' + `/${data.job.id}`);
        } else {
            const res = await resp.json();
            formErrors = res.data;
                }
            }
</script>

<svelte:head>
    <title>Edit Job Post</title>
</svelte:head>

<div class="flex justify-center items-center mt-8">
    <form on:submit={updateJob} class="w-2/3">
        <!-- Job Title Input -->
        <div class="form-control w-full">
            <label class="label" for="title">
                <span class="label-text">Job Title</span>
            </label>
            <input type="text" 
                   name="title"  
                   class="input input-bordered w-full"
                   value={data.job.title} />
            {#if 'title' in formErrors}
            <label class="label" for="title">
                <span class="label-text-alt text-red-500">{formErrors['title'].message}</span>
            </label>
            {/if}
          </div>

          <!-- Employer Input -->
        <div class="form-control w-full">
            <label class="label" for="employer">
                <span class="label-text">Employer</span>
            </label>
            <input type="employer" 
                   name="employer" 
                   class="input input-bordered w-full" 
                   value={data.job.employer} />
            {#if 'employer' in formErrors}
            <label class="label" for="employer">
                <span class="label-text-alt text-red-500">{formErrors['employer'].message}</span>
            </label>
            {/if}
        </div>

        <!-- Min. Annual Compensation Input -->
        <div class="form-control w-full">
            <label class="label" for="minAnnualCompensation">
                <span class="label-text">Min. Annual Salary</span>
            </label>
            <input type="minAnnualCompensation" 
                   name="minAnnualCompensation" 
                   class="input input-bordered w-full" 
                   value={data.job.minAnnualCompensation} />
            {#if 'minAnnualCompensation' in formErrors}
            <label class="label" for="minAnnualCompensation">
                <span class="label-text-alt text-red-500">{formErrors['minAnnualCompensation'].message}</span>
            </label>
            {/if}
        </div>

        <!-- Max. Annual Compensation Input -->
        <div class="form-control w-full">
            <label class="label" for="maxAnnualCompensation">
                <span class="label-text">Max. Annual Salary</span>
            </label>
            <input type="maxAnnualCompensation" 
                   name="maxAnnualCompensation" 
                   class="input input-bordered w-full" 
                   value={data.job.maxAnnualCompensation} />
            {#if 'maxAnnualCompensation' in formErrors}
            <label class="label" for="maxAnnualCompensation">
                <span class="label-text-alt text-red-500">{formErrors['maxAnnualCompensation'].message}</span>
            </label>
            {/if}
        </div>

        <!-- Location Input -->
        <div class="form-control w-full">
            <label class="label" for="location">
                <span class="label-text">Location</span>
            </label>
            <input type="location" 
                   name="location" 
                   class="input input-bordered w-full"
                   value={data.job.location} />
            {#if 'location' in formErrors}
            <label class="label" for="location">
                <span class="label-text-alt text-red-500">{formErrors['location'].message}</span>
            </label>
            {/if}
        </div>

        <!-- Description Input  -->
        <div class="form-control w-full">
            <label class="label" for="description">
                <span class="label-text">Description</span>
            </label>
            <textarea
                   type="text" 
                   name="description"
                   rows="5" 
                   class="textarea textarea-bordered w-full" 
                   value={data.job.description} />
            {#if 'description' in formErrors}
            <label class="label" for="description">
                <span class="label-text-alt text-red-500">{formErrors['description'].message}</span>
            </label>
            {/if}
        </div>

        <!-- Requirements Input -->
        <div class="form-control w-full">
            <label class="label" for="requirements">
                <span class="label-text">Experience Required</span>
            </label>
            <textarea
                   type="text" 
                   name="requirements" 
                   rows="5"
                   class="textarea textarea-bordered w-full" 
                   value={data.job.requirements} />
            {#if 'requirements' in formErrors}
            <label class="label" for="requirements">
                <span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
            </label>
            {/if}
        </div>

        <!-- Application Instructions Input -->
        <div class="form-control w-full">
            <label class="label" for="applicationInstructions">
                <span class="label-text">How To Apply</span>
            </label>
            <textarea
                   type="text" 
                   name="applicationInstructions" 
                   rows="3"
                   class="textarea textarea-bordered w-full" 
                   value={data.job.applicationInstructions} />
            {#if 'applicationInstructions' in formErrors}
            <label class="label" for="applicationInstructions">
                <span class="label-text-alt text-red-500">{formErrors['applicationInstructions'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Edit Job Post</button>
        </div>
    </form>
</div>

  
