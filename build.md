1. Run the following command to sign in:

   ```
   ssh root@oseccs.bne.redhat.com
   ```

2. Enter the following password: 

   ```
   redhat1!
   ```

3. Run the following to change your directory: 

   ```
   cd/root/sync/
   ```

4. Run the follwoing command, where `X.X doc_branch` is the version number and either `stage` for daily work, or `prod` for a live refresh or 

   ```
   ./acm_sync_asciidoc.sh <X.X X.X_branch>
   ```
   Example:

   ```
   ./acm_sync_asciidoc.sh 2.1 2.1_stage 
   ```
