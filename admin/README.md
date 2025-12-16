import React from 'react';
import { useForm } from 'react-hook-form';

type ThemeFormData = {
  name: string;
  description: string;
  // isActive: boolean; // This line may exist in types, but no change is specified here
};

type ThemeFormProps = {
  onSubmit: (data: ThemeFormData) => void;
  defaultValues?: Partial<ThemeFormData>;
};

const ThemeForm: React.FC<ThemeFormProps> = ({ onSubmit, defaultValues }) => {
  const { register, handleSubmit, formState: { errors } } = useForm<ThemeFormData>({
    defaultValues: {
      name: '',
      description: '',
      // isActive: true,  // Removed as per instruction
      ...defaultValues,
    },
  });

  const submitHandler = (formData: ThemeFormData) => {
    const payload = {
      name: formData.name,
      description: formData.description,
      // isActive: formData.isActive,  // Removed as per instruction
    };
    onSubmit(payload);
  };

  return (
    <form onSubmit={handleSubmit(submitHandler)}>
      <div>
        <label htmlFor="name">テーマ名</label>
        <input id="name" {...register('name', { required: true })} />
        {errors.name && <span>名前は必須です</span>}
      </div>

      <div>
        <label htmlFor="description">説明</label>
        <textarea id="description" {...register('description')} />
      </div>

      <div>
        <label htmlFor="isActive">有効化</label>
        <input id="isActive" type="checkbox" {...register('isActive')} />
      </div>

      <button type="submit">保存</button>
    </form>
  );
};

export default ThemeForm;
