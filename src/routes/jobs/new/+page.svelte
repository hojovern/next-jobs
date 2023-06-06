<script>
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { getUserId } from '../../../utils/auth.js';
    import { goto } from '$app/navigation';
    let formErrors = {};
  
    async function createJob(evt) {
		evt.preventDefault();
		
		const jobData = {
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

		await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
        method: 'POST',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(jobData)
      });
  
        goto ('/');

      }
</script>
  
  <div class="flex justify-center items-center mt-8">
      <form on:submit={createJob} class="w-2/3">
          <div class="form-control w-full">
              <label class="label" for="title">
                  <span class="label-text">Job Title</span>
              </label>
              <input type="text" 
                     name="title" 
                     placeholder="eg. Sulphur Miner" 
                     class="input input-bordered w-full" />
              <!-- {#if 'title' in formErrors}
              <label class="label" for="title">
                  <span class="label-text-alt text-red-500">{formErrors['title'].message}</span>
              </label>
              {/if} -->
            </div>
          
          <div class="form-control w-full">
              <label class="label" for="employer">
                  <span class="label-text">Employer</span>
              </label>
              <input type="employer" 
                     name="employer" 
                     placeholder="eg. Sulphur Mines Wonderland" 
                     class="input input-bordered w-full" 
                     required />
              <!-- {#if 'employer' in formErrors}
              <label class="label" for="employer">
                  <span class="label-text-alt text-red-500">{formErrors['employer'].message}</span>
              </label>
              {/if} -->
          </div>
  
          <div class="form-control w-full">
              <label class="label" for="minAnnualCompensation">
                  <span class="label-text">Min. Annual Salary</span>
              </label>
              <input type="minAnnualCompensation" 
                     name="minAnnualCompensation" 
                     placeholder="10,000" 
                     class="input input-bordered w-full" 
                     required />
              {#if 'minAnnualCompensation' in formErrors}
              <label class="label" for="minAnnualCompensation">
                  <span class="label-text-alt text-red-500">{formErrors['minAnnualCompensation'].message}</span>
              </label>
              {/if}
          </div>
  
          <div class="form-control w-full">
              <label class="label" for="maxAnnualCompensation">
                  <span class="label-text">Max. Annual Salary</span>
              </label>
              <input type="maxAnnualCompensation" 
                     name="maxAnnualCompensation" 
                     placeholder="50,000" 
                     class="input input-bordered w-full" 
                     required />
              <!-- {#if 'maxAnnualCompensation' in formErrors}
              <label class="label" for="maxAnnualCompensation">
                  <span class="label-text-alt text-red-500">{formErrors['maxAnnualCompensation'].message}</span>
              </label>
              {/if} -->
          </div>

          <div class="form-control w-full">
            <label class="label" for="location">
                <span class="label-text">Location</span>
            </label>
            <input type="location" 
                   name="location" 
                   placeholder="eg. Indonesia" 
                   class="input input-bordered w-full" 
                   required />
            <!-- {#if 'location' in formErrors}
            <label class="label" for="location">
                <span class="label-text-alt text-red-500">{formErrors['location'].message}</span>
            </label>
            {/if} -->
        </div>

        <div class="form-control w-full">
            <label class="label" for="description">
                <span class="label-text">Description</span>
            </label>
            <textarea
                   type="text" 
                   name="description"
                   placeholder="eg. Candidate will be required to mine sulphur in Indonesia." 
                   rows="5" 
                   class="textarea textarea-bordered w-full" 
                   required />
            <!-- {#if 'description' in formErrors}
            <label class="label" for="description">
                <span class="label-text-alt text-red-500">{formErrors['description'].message}</span>
            </label>
            {/if} -->
        </div>

        <div class="form-control w-full">
            <label class="label" for="requirements">
                <span class="label-text">Experience Required</span>
            </label>
            <textarea
                   type="text" 
                   name="requirements" 
                   placeholder="eg. Mined gold in Nicaragua for 3 years" 
                   rows="5"
                   class="textarea textarea-bordered w-full" 
                   required />
            <!-- {#if 'requirements' in formErrors}
            <label class="label" for="requirements">
                <span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
            </label>
            {/if} -->
        </div>

        <div class="form-control w-full">
            <label class="label" for="applicationInstructions">
                <span class="label-text">How To Apply</span>
            </label>
            <textarea
                   type="text" 
                   name="applicationInstructions" 
                   placeholder="eg. Send in a video demonstrating your mining skills" 
                   rows="3"
                   class="textarea textarea-bordered w-full" 
                   required />
            <!-- {#if 'applicationInstructions' in formErrors}
            <label class="label" for="applicationInstructions">
                <span class="label-text-alt text-red-500">{formErrors['applicationInstructions'].message}</span>
            </label>
            {/if} -->
        </div>
  
          <div class="form-control w-full mt-4">
              <button class="btn btn-md">Create a Job</button>
          </div>
      </form>
  </div>

 